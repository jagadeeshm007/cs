---
tags: [system-design, architecture, patterns]
phase: 3
---
# 🏗️ Architecture Patterns

## Macro architecture
| Pattern | Use when | Watch out for |
|---|---|---|
| Layered monolith | Tiny apps | Big ball of mud |
| **Modular monolith** | Default for new products | Needs module boundaries enforced (ArchUnit, Spring Modulith) |
| Microservices | Multiple teams, independent scaling/deploys | Distributed-systems tax: network, consistency, ops |
| Event-driven | Decoupling, fan-out, audit, async workflows | Eventual consistency, debugging, schema evolution |
| Serverless | Spiky workloads, glue | Cold starts, vendor lock-in, limits |
| Cell-based | Very large scale, blast-radius isolation | Routing, operational complexity |
| Space-based / in-memory grid | Extreme read/write loads | Complexity |

## Inside a service
- **Hexagonal (ports & adapters)** / **Clean Architecture**: domain in the center, frameworks at the edges
- **DDD tactical**: entities, value objects, aggregates (consistency boundary!), domain events, repositories
- **Vertical slice architecture**: organize by feature, not by layer

## Integration & data patterns
- [ ] **Transactional outbox** (+ CDC via Debezium) to publish events reliably
- [ ] **Saga**: choreography vs orchestration; compensating actions
- [ ] **CQRS**: separate write model and read models (projections)
- [ ] **Event sourcing**: state = fold(events); snapshots; when it's worth it (rarely)
- [ ] **Idempotent consumer / inbox pattern**
- [ ] **API composition / BFF (backend for frontend)**
- [ ] **Strangler fig** (incremental migration from a monolith)
- [ ] **Anti-corruption layer**
- [ ] **Database per service** vs shared DB
- [ ] **Durable execution** (Temporal) as an alternative to hand-rolled sagas

## Resilience patterns (*Release It!*)
Timeouts · retries with exponential backoff + jitter · circuit breaker · bulkhead · rate limiting · load shedding · fallback/graceful degradation · health checks · backpressure · idempotency keys

## Deployment patterns
Blue/green · canary · rolling · feature flags (OpenFeature) · dark launches · expand/contract DB migrations

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟡 Spring Modulith boundaries + ArchUnit rules in orbit-api
- [ ] 🔴 Outbox → Debezium → Kafka with an inbox dedupe on the consumer
- [ ] 🔴 Orchestrated saga with compensation (UC3); then port it to Temporal and compare
- [ ] ⚫ Rebuild the run-search read model from zero by replaying Kafka (CQRS rebuild)

## 🧠 Cognitive tasks
- [ ] Trade-off debate: event sourcing for runs vs a state table + audit log
- [ ] Pre-mortem: 10 ways the saga leaves inconsistent state

## 🛰️ Orbit integration
- [ ] Hexagonal engine core; CQRS run search; a strangler-fig split of orbit-api later

> [!info] Go deeper
> 🧩 [[Enterprise & DDD Patterns]] · [[Distributed & Cloud Patterns]] · [[AI & Agent Patterns]]

## Resources
- *Fundamentals of Software Architecture* 2e (Richards & Ford) ⭐
- *Software Architecture: The Hard Parts* (Ford et al.) ⭐
- *Microservices Patterns* (Richardson) + microservices.io ⭐
- *Building Microservices* 2e + *Monolith to Microservices* (Newman)
- *Learning Domain-Driven Design* (Khononov) · *Domain-Driven Design Distilled* (Vernon)
- *Enterprise Integration Patterns* (Hohpe & Woolf): reference
- *A Philosophy of Software Design* (Ousterhout) ⭐: code-level design thinking
