---
tags: [cs, networking]
phase: 1
---
# 🌐 Networking

## Core → Advanced
- [ ] OSI vs TCP/IP model; what L4 and L7 mean (matters for load balancers)
- [ ] IP, subnets/CIDR, NAT, private ranges (needed for VPCs in AWS)
- [ ] TCP: 3-way handshake, flow control, congestion control, TIME_WAIT, Nagle, keep-alive
- [ ] UDP and when to use it; QUIC
- [ ] DNS resolution chain, TTLs, record types (A, AAAA, CNAME, SRV, TXT)
- [ ] HTTP/1.1 (keep-alive, head-of-line blocking) → HTTP/2 (multiplexing, HPACK) → HTTP/3 (QUIC)
- [ ] TLS 1.3 handshake, certificates, CA chain, mTLS, SNI
- [ ] Load balancing: L4 vs L7, algorithms (round robin, least-conn, consistent hashing), health checks
- [ ] CDNs, anycast, edge caching, cache headers (`Cache-Control`, `ETag`)
- [ ] WebSockets, SSE, long polling ([[Realtime (WebSockets, SSE)]])
- [ ] Proxies: forward vs reverse, connection pooling, timeouts ([[Envoy, Gateways & Service Mesh]])

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 `dig +trace`, `curl -v --http2`, `curl -w` timing breakdown; explain every line
- [ ] 🟡 HTTP/1.1 server from raw TCP in Go (keep-alive, chunked encoding)
- [ ] 🟡 Wireshark + `SSLKEYLOGFILE`: decrypt TLS 1.3 and read HTTP/2 frames
- [ ] 🔴 An L7 load balancer in Go (codingchallenges.fyi): health checks, round robin, least-conn
- [ ] 🔴 A DNS resolver in Go that walks from the root servers
- [ ] ⚫ A TCP proxy with connection pooling; measure the latency win vs no pooling

## 🧠 Cognitive tasks
- [ ] Blank-page: "what happens when you type a URL" in 15 min at full depth
- [ ] Predict → verify: time saved per request by connection reuse from Mumbai to us-east-1
- [ ] First-principles: why does HTTP/2 still have head-of-line blocking?

## 🛰️ Orbit integration
- [ ] SSE streaming through proxies (buffering, idle timeouts) for orbit-stream
- [ ] gRPC load balancing between orbit-api and the engine (why L4 fails)

> [!info] Go deeper
> ⚙️ [[Network Stack Internals]] · [[Envoy Internals]]

## Resources
- *High Performance Browser Networking* (Grigorik, free at hpbn.co): ⭐ best practical book
- *Computer Networking: A Top-Down Approach* (Kurose & Ross): reference
- Beej's Guide to Network Programming
- Cloudflare Learning Center (free and excellent)

## Interview questions #interview-q
- What happens when you type `google.com` and press Enter? (Go deep: DNS → TCP → TLS → HTTP → LB → server → render)
- Why does HTTP/2 still suffer from head-of-line blocking at the TCP level?
- L4 vs L7 load balancer?
