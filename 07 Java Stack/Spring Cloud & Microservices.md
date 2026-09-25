---
tags: [java, spring, microservices]
phase: 3
---
# ☁️ Spring Cloud & Microservices (Java)

## Checklist
- [ ] **Resilience4j**: circuit breaker, retry, rate limiter, bulkhead, time limiter
- [ ] Spring Cloud Gateway (vs Envoy/Kong: know the trade-off)
- [ ] Service discovery: Eureka vs **Kubernetes-native DNS** (prefer K8s in 2026)
- [ ] Spring Cloud Config vs K8s ConfigMaps/Secrets + external secrets
- [ ] **Spring for Apache Kafka**: `KafkaTemplate`, `@KafkaListener`, error handlers, DLT, retries, transactions
- [ ] Spring Cloud Stream (awareness)
- [ ] gRPC in Spring (Spring gRPC project / grpc-java)
- [ ] Spring for GraphQL
- [ ] Distributed tracing with Micrometer Tracing + OTel
- [ ] Contract testing: Spring Cloud Contract or Pact
- [ ] Temporal Java SDK for orchestrated sagas (optional but valuable)

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟡 Resilience4j: circuit breaker + retry + bulkhead around provider/tool calls; chaos-test it
- [ ] 🔴 Spring Kafka consumers with retry topics + a DLT + an idempotent inbox
- [ ] 🔴 Contract tests between orbit-api and orbit-tools
- [ ] ⚫ Temporal Java SDK version of UC3; compare it with Orbit's engine

## 🧠 Cognitive tasks
- [ ] Pre-mortem: what happens when orbit-tools is down for 10 minutes?

## 🛰️ Orbit integration
- [ ] orbit-tools and orbit-knowledge as separate Spring services from v2 onward

> [!info] Go deeper
> ⚙️ [[Kafka Internals]] · 🧩 [[Distributed & Cloud Patterns]]

