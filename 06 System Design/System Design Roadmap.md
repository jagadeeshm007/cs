---
tags: [system-design, roadmap, moc]
---
# 🏛️ System Design Roadmap: core → advanced

## Level 1: Fundamentals (Phases 1–2)
- [ ] Client–server, HTTP, REST, stateless services
- [ ] Vertical vs horizontal scaling; load balancers
- [ ] SQL vs NoSQL; indexes; replication basics
- [ ] Caching layers (browser, CDN, app, DB); cache-aside
- [ ] [[Estimation Cheatsheet]]

## Level 2: Building blocks (Phases 2–3) → [[Building Blocks]]
- [ ] Load balancer, API gateway, reverse proxy
- [ ] Cache (Redis), CDN, object storage (S3)
- [ ] Message queue vs event log (SQS/RabbitMQ vs Kafka)
- [ ] Search index, rate limiter, ID generator, distributed lock
- [ ] Blob + metadata split; presigned URLs

## Level 3: Distributed systems (Phase 3) → [[Distributed Systems]]
- [ ] Replication, partitioning/sharding, consistent hashing
- [ ] Consistency models, CAP/PACELC, quorums
- [ ] Consensus (Raft), leader election, clocks
- [ ] Idempotency, exactly-once illusions, ordering

## Level 4: Architecture patterns (Phase 3) → [[Architecture Patterns]]
- [ ] Monolith → modular monolith → microservices
- [ ] Event-driven, CQRS, event sourcing, saga, outbox
- [ ] DDD strategic design (bounded contexts, context maps)
- [ ] Hexagonal / clean architecture (inside a service)
- [ ] Resilience: timeouts, retries, circuit breakers, bulkheads, load shedding

## Level 5: Production & scale (Phases 4–6)
- [ ] Multi-region, active-active vs active-passive, cell-based architecture
- [ ] Observability, SLOs, capacity planning
- [ ] Zero-downtime deployments, schema migrations (expand/contract), feature flags
- [ ] Cost-aware architecture
- [ ] AI systems architecture (RAG, agents, LLM gateways) → [[AI Engineering Roadmap]]

## 🎤 Interview framework (45–60 min)
| Step | Time | Output |
|---|---|---|
| 1. Requirements | 5 min | Functional (3–5 core features), non-functional (scale, latency, availability, consistency) |
| 2. Estimates | 3 min | QPS (avg/peak), storage/yr, bandwidth; only estimate what drives decisions |
| 3. API | 5 min | Key endpoints/events |
| 4. Data model | 5 min | Entities, keys, access patterns → DB choice |
| 5. High-level design | 10 min | Boxes and arrows covering every functional requirement |
| 6. Deep dives | 15 min | The 2–3 hardest parts (contention, hot keys, fan-out, consistency) |
| 7. Wrap-up | 5 min | Bottlenecks, failure modes, monitoring, evolution |

> [!tip] What interviewers score
> Structured approach · clear trade-offs · depth in 1–2 areas · handling of failures · communication. **Not** the number of boxes.

## Resources
- ⭐ *DDIA* · *System Design Interview* Vol 1 & 2 (Xu) · *Understanding Distributed Systems* (Vitillo)
- ⭐ **Hello Interview** (written deep dives + guided practice) · ByteByteGo · *system-design-primer* (GitHub)
- YouTube: Jordan Has No Life, Hello Interview, ByteByteGo, Gaurav Sen (intro)
- Real architectures: [[Engineering Blogs & Papers]]
- Practice: [[Case Studies]] (use the *System Design Case* template)
