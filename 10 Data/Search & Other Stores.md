---
tags: [data, search, nosql]
phase: 3
---
# 🔎 Search & Other Datastores

## Search (OpenSearch / Elasticsearch)
- [ ] Inverted index, analyzers, tokenization, BM25 relevance
- [ ] Mappings, shards & replicas, refresh interval (near real-time)
- [ ] Queries: match, bool, filters vs queries, aggregations, facets
- [ ] Keeping search in sync: dual writes (bad) vs **CDC/events** (good); reindexing with aliases
- [ ] Hybrid search (BM25 + vectors) → [[RAG]]

## NoSQL landscape (know when and why)
| Store | Model | Pick when |
|---|---|---|
| DynamoDB | KV/wide-column, single-table design | AWS, predictable access patterns, massive scale |
| Cassandra/ScyllaDB | Wide-column, leaderless | Write-heavy, multi-DC, time series |
| MongoDB | Document | Flexible schema, rapid iteration |
| ClickHouse | Columnar OLAP | Analytics, logs, events |
| Neo4j | Graph | Relationship-heavy queries |
| TimescaleDB/InfluxDB | Time series | Metrics, IoT |
| Vector DBs (pgvector, Qdrant, Milvus, Weaviate) | Vectors | Semantic search, RAG |

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟡 An OpenSearch run-search projection from Kafka (rebuildable)
- [ ] 🔴 BM25 from scratch in Go vs Postgres FTS vs OpenSearch on the same corpus
- [ ] ⚫ A DynamoDB single-table design for Orbit runs (on paper + a local DynamoDB)

## 🧠 Cognitive tasks
- [ ] Trade-off debate: pgvector vs a dedicated vector DB for 10M chunks

## 🛰️ Orbit integration
- [ ] Run search, hybrid retrieval, and ClickHouse analytics

> [!info] Go deeper
> ⚙️ [[LLM Inference Internals]] (HNSW)

