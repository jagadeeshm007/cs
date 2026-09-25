---
tags: [infra, envoy, gateway, service-mesh]
phase: 4
---
# 🚪 Envoy, API Gateways & Service Mesh

## Concepts
- [ ] Reverse proxy vs load balancer vs API gateway vs service mesh: draw the difference
- [ ] North–south (edge) vs east–west (service-to-service) traffic
- [ ] **Envoy** architecture: listeners → filter chains → routes → clusters → endpoints; xDS dynamic config
- [ ] Envoy features: retries, timeouts, circuit breaking, outlier detection, rate limiting (local + global), JWT authn, ext_authz, gRPC-JSON transcoding, observability
- [ ] **Kubernetes Gateway API** (`Gateway`, `HTTPRoute`, `GRPCRoute`) ⭐ the modern standard
- [ ] Implementations: **Envoy Gateway**, Istio, Kong, NGINX Gateway Fabric, Traefik, AWS ALB
- [ ] Note: the community ingress-nginx controller is being retired; plan on Gateway API
- [ ] API gateway responsibilities: auth, rate limits, routing, request transformation, API keys, quotas
- [ ] Service mesh: **Istio** (sidecar vs **ambient mode**), Linkerd; mTLS, traffic splitting, retries, telemetry
- [ ] When NOT to use a mesh (complexity, latency, operational burden)
- [ ] **AI gateways / LLM gateways**: routing, rate limits, and cost control for LLM calls (Envoy AI Gateway, LiteLLM, Kong AI)

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 Standalone Envoy: routing + retries + a local rate limit; read `/config_dump`
- [ ] 🟡 Envoy Gateway + Gateway API routes + JWT authn
- [ ] 🔴 An **ext_authz server in Go** for Orbit API keys
- [ ] 🔴 Circuit breaking + outlier detection experiments; a retry budget
- [ ] ⚫ An AI gateway via ext_proc: token counting / PII redaction at the edge (compare with your Go gateway)

## 🧠 Cognitive tasks
- [ ] Trade-off debate: put LLM quota logic in Envoy vs in orbit-llm-gateway?

## 🛰️ Orbit integration
- [ ] The Orbit edge (v3)

> [!info] Go deeper
> ⚙️ [[Envoy Internals]] · [[Network Stack Internals]]

## Resources
- envoyproxy.io docs + "Envoy fundamentals" · gateway-api.sigs.k8s.io · istio.io docs
- Matt Klein's blog posts on Envoy and service mesh
