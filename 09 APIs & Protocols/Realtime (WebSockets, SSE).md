---
tags: [api, realtime]
---
# 📡 Realtime: WebSockets, SSE, long polling

| Tech | Direction | Use case |
|---|---|---|
| Short/long polling | Client pulls | Simple, fallback |
| **SSE** | Server → client over HTTP | Notifications, **LLM token streaming** ⭐, live scores |
| **WebSockets** | Bidirectional | Chat, collaborative editing, live seat maps |
| WebTransport / QUIC | Bidirectional, multiplexed | Emerging |
| gRPC streaming | Service ↔ service | Internal streams |

## Scaling concerns
- Sticky sessions vs a shared pub/sub (Redis pub/sub, Kafka, NATS) to fan out across nodes
- Connection limits per node (file descriptors, memory per connection)
- Heartbeats, reconnection with backoff, resuming from the last event ID
- Presence systems

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟡 SSE token streaming with `Last-Event-ID` resume
- [ ] 🔴 Fan-out across 3 orbit-stream replicas via Redis pub/sub
- [ ] ⚫ 5,000 concurrent SSE connections: measure memory per connection and tune timeouts

## 🧠 Cognitive tasks
- [ ] Predict which proxy setting breaks a 5-minute stream first

## 🛰️ Orbit integration
- [ ] orbit-stream: tokens + run events to orbit-web; the approvals inbox live updates

> [!info] Go deeper
> ⚙️ [[Network Stack Internals]] · [[Envoy Internals]]

