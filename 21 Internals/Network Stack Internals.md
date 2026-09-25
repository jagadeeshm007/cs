---
tags: [internals, networking, grpc, http2, tls]
week: W3–W4, W8
---
# 🌐 Network Stack Internals: TCP · TLS · HTTP/2 · gRPC

## 1. Sockets in the kernel
- `listen()` creates two queues: the **SYN queue** (half-open) and the **accept queue** (established, waiting for `accept()`); overflow → dropped SYNs → client retries after 1 s+ → **mysterious 1 s/3 s latency**
- `SO_REUSEPORT` lets multiple processes/threads accept on the same port (kernel load-balances)
- **epoll**: register fds, get readiness events → one thread serves thousands of connections (Netty, Go netpoller, Envoy, Redis, Nginx)

## 2. TCP essentials
- 3-way handshake = 1 RTT before any data · **slow start**: `cwnd` starts small (~10 segments) and grows → new connections are slow → **reuse connections (pooling, keep-alive)**
- Flow control (receiver window) vs congestion control (CUBIC, **BBR**)
- **Nagle + delayed ACK** can add ~40 ms per small write → `TCP_NODELAY` (on by default in Go; set it in many Java clients)
- **TIME_WAIT** (2×MSL) on the side that closes first → **ephemeral port exhaustion** under high connection churn → pooling
- TCP head-of-line blocking: one lost packet stalls all data behind it (even for HTTP/2 streams)

## 3. TLS 1.3
- **1-RTT handshake**: ClientHello (+ key share, SNI, **ALPN** offers `h2`) → ServerHello + certificate + Finished (encrypted) → the client sends data
- **0-RTT** resumption: faster, but early data can be **replayed** → only for idempotent requests
- mTLS: the client presents a certificate too (service mesh identity)
- Cost: handshake CPU + RTTs → terminate at the edge and reuse connections

## 4. HTTP/2
- One TCP connection, many **streams**; binary **frames**: `HEADERS`, `DATA`, `SETTINGS`, `WINDOW_UPDATE`, `RST_STREAM`, `PING`, `GOAWAY`
- **HPACK** header compression (static + dynamic tables)
- **Flow control** per stream and per connection (`WINDOW_UPDATE`) → a slow reader can stall a stream
- `GOAWAY` for graceful connection draining (important during deploys)

## 5. gRPC on the wire
- Every call = an HTTP/2 **POST** to `/package.Service/Method`, `content-type: application/grpc`
- Messages are **length-prefixed**: 1 byte compressed flag + 4 bytes length + the protobuf bytes
- Status comes back in **trailers** (`grpc-status`, `grpc-message`); deadlines travel in the `grpc-timeout` header and **propagate**
- Streaming = many messages on one HTTP/2 stream; keepalive = HTTP/2 PING
- **LB gotcha**: one long-lived connection multiplexes everything → an L4 load balancer pins all traffic to one backend → use L7 (Envoy) or client-side LB (xDS/DNS round-robin with multiple subconns)

## 6. HTTP/3 / QUIC
UDP-based; streams are independent (**no TCP HOL blocking**); combined transport+TLS handshake (1-RTT, 0-RTT); connection migration (Wi-Fi → mobile)

## 7. DNS in practice
- Resolver caching layers: app (JVM `networkaddress.cache.ttl`), OS (systemd-resolved), CoreDNS in K8s (`ndots:5` → many extra lookups!)
- Low TTLs for failover vs load on DNS

## 🔬 Prove it
- [ ] Wireshark + `SSLKEYLOGFILE` to decrypt TLS and view HTTP/2 frames of a gRPC call (see the 5-byte prefix and trailers)
- [ ] `ss -tan state time-wait | wc -l` during a load test **without** keep-alive vs with pooling
- [ ] Nagle experiment: a Java client with 2 small writes per request, with/without `TCP_NODELAY`
- [ ] `GODEBUG=http2debug=2` in a Go gRPC client: read the frame log
- [ ] gRPC behind a K8s ClusterIP with 3 pods → all traffic hits 1 pod → fix it with Envoy or headless Service + round_robin
- [ ] `curl -w '%{time_connect} %{time_appconnect} %{time_starttransfer}'` against a far region: attribute the latency to TCP, TLS, and server

## Interview questions #interview-q
What happens when you type a URL (full depth) · HTTP/1.1 vs 2 vs 3 · the TLS 1.3 handshake · why connection pooling matters · gRPC load-balancing problems · TIME_WAIT
