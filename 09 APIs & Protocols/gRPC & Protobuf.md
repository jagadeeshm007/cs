---
tags: [api, grpc, protobuf]
phase: 2
---
# ⚡ gRPC & Protocol Buffers

## Checklist
- [ ] Protobuf proto3: scalar types, `oneof`, `repeated`, `map`, well-known types (`Timestamp`, `Duration`, `FieldMask`)
- [ ] Wire format basics (varints, field numbers) and why it's compact
- [ ] **Schema evolution rules**: never reuse field numbers, `reserved`, adding fields is safe
- [ ] **buf**: lint, breaking-change detection, codegen, BSR ⭐
- [ ] gRPC over HTTP/2: unary, server streaming, client streaming, bidi streaming
- [ ] Deadlines/timeouts & propagation; cancellation
- [ ] Status codes, rich error details
- [ ] Interceptors (auth, logging, metrics, tracing)
- [ ] Load balancing gotcha: long-lived HTTP/2 connections → need L7 (Envoy) or client-side LB
- [ ] gRPC-Gateway / **Connect** (gRPC + HTTP/JSON from browsers)
- [ ] Health checking protocol, reflection, `grpcurl`
- [ ] Protobuf as the Kafka event schema (with a Schema Registry)

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 A `proto/` module with buf lint + breaking checks in CI
- [ ] 🟡 A Java client ↔ Go server with deadlines + interceptors
- [ ] 🔴 Server-streaming run events (engine → api)
- [ ] ⚫ The load-balancing gotcha on K8s: reproduce it, then fix it with Envoy or client-side LB

## 🧠 Cognitive tasks
- [ ] Wireshark a gRPC call: find the 5-byte prefix and `grpc-status` trailers

## 🛰️ Orbit integration
- [ ] orbit-api ↔ engine ↔ worker contracts; Protobuf Kafka events

> [!info] Go deeper
> ⚙️ [[Network Stack Internals]] · [[Envoy Internals]]

## Resources
- grpc.io docs · protobuf.dev · buf.build docs · *gRPC: Up and Running*
