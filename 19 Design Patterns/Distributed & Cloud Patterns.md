---
tags: [patterns, distributed, cloud, microservices]
---
# 🌍 Distributed & Cloud Patterns

## A. Patterns of distributed systems (Unmesh Joshi) ⭐
| Pattern | Problem → solution | Where you've seen it | Orbit |
|---|---|---|---|
| **Write-ahead log** | Durability → log before applying | Postgres WAL, Kafka | Run event history |
| **Segmented log** | Huge logs → split into segments | Kafka segments | History partitioning |
| **Low/high-water mark** | What's safe to read or delete | Kafka HW, Postgres checkpoints | Consumer progress |
| **Leader & followers** | Single writer | Kafka, Postgres | — |
| **Heartbeat** | Detect failure | K8s node leases | Worker heartbeats |
| **Lease** ⭐ | Time-bound ownership | etcd, K8s leader election | Task leases |
| **Fencing token / generation clock** ⭐ | Reject stale owners | Raft terms, Kafka leader epochs | Lease epoch checked on step completion |
| **Quorum** | Majority agreement | Raft, Dynamo | — |
| **Idempotent receiver** ⭐ | Dedupe retries | Kafka idempotent producer | Tool calls with idempotency keys |
| **Request pipeline / batching** | Throughput | Kafka producer, Redis pipelining | Embedding batches |
| **Consistent hashing** | Rebalance with minimal movement | Dynamo, Cassandra, Envoy ring hash | Sticky routing of runs to engine shards |
| **Gossip dissemination** | Cluster membership | Cassandra, Redis Cluster | — |
| **Version vector / Lamport clock** | Ordering without synchronized clocks | Dynamo | Event ordering discussion |

## B. Reliability & resilience
Timeout ⭐ · **Retry with exponential backoff + jitter** ⭐ · **Circuit breaker** · **Bulkhead** · **Rate limiting / throttling** · **Load shedding** · Fallback / graceful degradation · Health endpoint monitoring · **Retry budget** · **Idempotency key** · Hedged requests (tail latency) · Deadline propagation

## C. Messaging & data
| Pattern | Use | Orbit |
|---|---|---|
| **Transactional outbox** ⭐ | Atomically update the DB + publish an event (no **dual writes**) | api + engine |
| **Inbox** | Consumer-side dedupe | hooks, notification |
| **Competing consumers** | Scale a queue horizontally | workers |
| **Queue-based load leveling** | Absorb spikes | task queue + KEDA |
| **Priority queue** | Premium tenants first | tenant tiers |
| **Sequential convoy** | Order per key, parallel across keys | Kafka key = runId |
| **Claim check** ⭐ | Keep large payloads out of messages (store in S3, pass a reference) | Documents, big LLM outputs |
| **Pub/Sub** | Fan-out | run events |
| **Dead letter queue** | Park poison messages | webhooks |
| **CQRS + materialized view** | Separate read models | run search in OpenSearch |
| **Event sourcing** | State = events | run history |
| **Saga / compensating transaction** ⭐ | Cross-service consistency | UC3 refunds |
| **Scheduler-agent-supervisor** ⭐ | Coordinate and recover distributed steps | **This is literally the Orbit engine** |
| **Pipes & filters** | Composable processing stages | Ingestion pipeline |
| **Sharding** | Scale writes | Event history by run_id hash |

## D. Edge, deployment & topology (cloud design patterns)
**API gateway** (routing, aggregation, **offloading** auth/TLS/rate limits) · **BFF** · **Sidecar** · **Ambassador** · **Anti-corruption layer** · **Strangler fig** · **Valet key** (presigned URLs) ⭐ · **Static content hosting/CDN** · **Deployment stamps / cell-based architecture** ⭐ · **Geode** (multi-region) · **Leader election** · **Operator (controller) pattern** ⭐ · Blue/green · Canary · Feature flags · **Expand/contract migrations**

## 🔬 Katas
- [ ] Implement a lease + fencing token with Postgres, then show a stale worker's write being rejected (simulate a GC pause with `SIGSTOP`)
- [ ] Retry storm simulation: 3 service layers × 3 retries = 27× amplification → fix with budgets + jitter
- [ ] Consistent hash ring with virtual nodes: measure key movement when adding a node (≈ 1/N)
- [ ] Hedged requests to an LLM provider: p99 improvement vs cost increase
- [ ] Claim-check refactor: move >256 KB step outputs to MinIO; measure Kafka throughput before/after
