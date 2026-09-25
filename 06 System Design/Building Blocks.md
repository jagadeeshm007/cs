---
tags: [system-design, building-blocks]
---
# 🧱 Building Blocks

For each block, know: **what it does, when to use it, how it scales, how it fails, and 2 real products.**

| Block | Purpose | Real products | Key concerns |
|---|---|---|---|
| DNS | Name → IP, geo routing | Route 53, Cloudflare | TTL, failover |
| CDN | Cache static/dynamic content at the edge | CloudFront, Cloudflare, Akamai | Invalidation, cache keys |
| Load balancer | Distribute traffic, health checks | ALB/NLB, Envoy, NGINX, HAProxy | L4 vs L7, sticky sessions, algorithms |
| API gateway | Auth, rate limiting, routing, aggregation | Kong, Envoy Gateway, AWS API GW, Spring Cloud Gateway | Single point of failure, latency |
| Service | Business logic | Your code | Stateless, horizontal scaling |
| Cache | Low-latency reads | Redis, Memcached, Caffeine | Invalidation, stampede, consistency |
| Relational DB | Source of truth, transactions | PostgreSQL, MySQL, Aurora | Scaling writes, schema migrations |
| Wide-column / KV | Massive scale, simple access | Cassandra, DynamoDB, ScyllaDB | Data modeling by query, hot partitions |
| Document DB | Flexible schema | MongoDB | Transactions, joins |
| Search | Full-text, facets, relevance | OpenSearch/Elasticsearch | Indexing lag, reindexing |
| Vector DB | Semantic similarity | pgvector, Qdrant, Weaviate, Pinecone | Recall vs latency, filtering |
| OLAP | Analytics | ClickHouse, BigQuery, Snowflake, Druid | Ingestion, columnar storage |
| Object storage | Blobs, files, backups, data lake | S3, GCS, MinIO | Presigned URLs, lifecycle |
| Queue | Task distribution | SQS, RabbitMQ | Visibility timeout, DLQ |
| Event log | Streaming, replay, fan-out | Kafka, Redpanda, Kinesis, Pulsar | Partitions, ordering, retention |
| Workflow engine | Durable, long-running processes | Temporal, AWS Step Functions | Determinism, versioning |
| Coordination | Leader election, config, locks | etcd, ZooKeeper | Consensus, quorum |
| ID generator | Unique, sortable IDs | Snowflake, UUIDv7, ULID | Clock skew |
| Rate limiter | Protect resources | Redis + token bucket, Envoy | Distributed counting |
| Notification | Push, email, SMS | FCM/APNs, SES, Twilio | Retries, dedupe, preferences |
| Observability | Metrics, logs, traces | Prometheus, Grafana, OTel, Loki, Tempo | Cardinality, cost |

## Must-know algorithms inside systems
Consistent hashing · Bloom filters · HyperLogLog · Count-Min sketch · Merkle trees · Geohash/quadtree/S2/H3 · Token bucket / leaky bucket / sliding window · Gossip protocols · Vector clocks · LSM trees · Skip lists

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟡 Build miniature versions: a rate limiter (W2), a KV cache (W1), an L7 LB (W3), a queue with leases (W10), an ID generator (Snowflake in Go)
- [ ] 🔴 Bloom filter + HyperLogLog + count-min sketch in Go with accuracy tests
- [ ] 🔴 Consistent hash ring with virtual nodes; measure key movement

## 🧠 Cognitive tasks
- [ ] For each block, write: how it scales, how it fails, and 2 real products that use it
- [ ] Reverse engineering: identify every building block in Orbit's architecture diagram

## 🛰️ Orbit integration
- [ ] Every block appears in Orbit; see the architecture in [[Orbit - Overview]]

> [!info] Go deeper
> ⚙️ [[Internals Roadmap]] · 🧩 [[Distributed & Cloud Patterns]]

