---
tags: [internals, envoy, gateway]
week: W16
---
# 🚪 Envoy Internals (important parts only)

## 1. Threading model
- **Main thread**: config (xDS), admin API, stats flushing, not on the data path
- **N worker threads** (≈ cores), each with its **own event loop**; a connection is **owned by one worker for its lifetime** → no locks on the hot path
- Config updates are pushed to workers via **thread-local storage** snapshots (RCU-like)
- Connection pools are **per worker, per upstream cluster** → with many workers you open more upstream connections than you'd expect

## 2. Request path
```
Listener (socket) → listener filters (tls_inspector, proxy_protocol)
  → filter chain match (SNI/ALPN/port)
    → network filters (e.g. http_connection_manager, tcp_proxy)
      → HTTP filters (cors, jwt_authn, ext_authz, ratelimit, lua/wasm/ext_proc … router)
        → router: route table match → cluster → load balancer → host → connection pool → upstream
```

## 3. xDS (dynamic configuration)
- **LDS** (listeners), **RDS** (routes), **CDS** (clusters), **EDS** (endpoints), **SDS** (secrets/certs); **ADS** multiplexes them on one gRPC stream for ordering
- State-of-the-world vs **incremental (delta)** xDS
- Control planes: Istio (istiod), Envoy Gateway, Contour, custom ones (go-control-plane ⭐ in Go)

## 4. Resilience features and how they behave
- **Timeouts**: route timeout, per-try timeout, idle timeout, stream idle timeout (⚠️ SSE/LLM streaming needs these tuned)
- **Retries**: `retry_on` conditions, a **retry budget** (a % of active requests) to prevent retry storms
- **Circuit breakers** (per cluster, per priority): max connections, max pending requests, max requests, max retries → returns 503 with `x-envoy-overloaded`
- **Outlier detection**: eject hosts after consecutive 5xx / high latency (passive health checking); plus active health checks
- Load balancing: round robin, least request (power of two choices), ring hash / Maglev (consistent hashing for stickiness)

## 5. Extensibility
C++ filters · Lua · **Wasm** · **ext_authz** (call your gRPC auth service) · **ext_proc** (stream request/response to an external processor, used by AI gateways for token counting/PII redaction)

## 6. Observability
Admin endpoint: `/config_dump`, `/clusters` (per-host health and stats), `/stats` (`upstream_rq_*`, `upstream_cx_*`, `cx_overflow`, `rq_pending_overflow`); access logs; native tracing

## 🔬 Prove it
- [ ] Standalone Envoy in front of 3 backends: read `/config_dump` and `/clusters`
- [ ] Set `max_pending_requests: 1` → load test → see `upstream_rq_pending_overflow` and 503s
- [ ] Make one backend return 5xx → watch outlier detection eject it
- [ ] Retry storm: aggressive retries on a slow backend → load amplification → cap it with a retry budget
- [ ] SSE through Envoy: find the timeout that kills long streams → fix it with route/stream idle timeouts
- [ ] **Write an ext_authz gRPC server in Go** that validates Orbit API keys → [[Assignments - Phase 4]]

## Interview questions #interview-q
L4 vs L7 proxying · how Envoy handles config updates without restarts · circuit breaking vs outlier detection · retry budgets · API gateway vs service mesh
