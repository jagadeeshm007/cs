---
tags: [mindset, system-design]
---
# ⚖️ Trade-offs Cheat Sheet

> [!tip] Interview superpower
> For every choice, say: **"I'm choosing X over Y because of constraint Z. The cost is W, and we'd revisit it if V happens."**

| Decision | Option A | Option B | Choose A when | Choose B when |
|---|---|---|---|---|
| Architecture | Modular monolith | Microservices | Small team, early product, unclear domain boundaries | Many teams, independent deploy/scale needs, clear bounded contexts |
| Consistency | Strong (linearizable) | Eventual | Money, inventory, seats, uniqueness | Feeds, counters, analytics, search |
| Communication | Sync (REST/gRPC) | Async (events/queues) | Needs an immediate answer, simple flows | Decoupling, spikes, fan-out, long-running work |
| Internal API | gRPC | REST | Service-to-service, streaming, strict contracts, performance | Public APIs, browsers, simplicity, caching |
| Client API | GraphQL | REST | Many clients with different data needs, aggregation | Simple resources, HTTP caching, simple ops |
| DB | Relational (Postgres) | NoSQL (Cassandra/Dynamo) | Relations, transactions, ad-hoc queries (**default choice**) | Massive write scale, known access patterns, multi-region AP |
| Scaling reads | Cache | Read replicas | Hot, repeated reads; tolerate staleness | Complex queries, fresher data |
| Cache writes | Cache-aside | Write-through / write-behind | General purpose | Read-after-write needs / write-heavy buffering |
| Concurrency control | Optimistic (version) | Pessimistic (`SELECT … FOR UPDATE`) | Low contention | High contention on the same rows |
| Delivery | At-least-once + idempotency | Exactly-once (Kafka txns) | Almost always | Stream-processing pipelines inside Kafka |
| Transactions across services | Saga | 2PC | Microservices (almost always) | Rare, single-vendor, tightly coupled resources |
| Queue | Kafka | RabbitMQ/SQS | Event streams, replay, high throughput, ordering per key | Task queues, routing, per-message ack, simpler ops |
| IDs | UUIDv7 / Snowflake | Auto-increment | Distributed, sortable, no coordination | Single DB, simplicity |
| Compute | Containers on K8s | Serverless | Steady load, many services, platform team | Spiky/low load, small team, event glue |
| Pagination | Cursor/keyset | Offset | Large/real-time data | Small datasets, jump-to-page UI |
| Language | Go | Java/Spring | Infra, high concurrency, small binaries, fast startup | Rich enterprise ecosystem, complex domains, big teams |

## Trade-off axes to always consider
Latency · Throughput · Consistency · Availability · Durability · Cost · Complexity · Operability · Security · Time-to-market · Reversibility · Team skill
