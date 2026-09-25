---
tags: [assignments, open-ended]
---
# 🌀 Open Assignments (no single right answer)

These are **research + build + write** challenges. Pick one whenever you finish a week early, and 2 in the W25–W26 buffer. Deliverable: prototype + benchmark/evidence + a 2-page write-up with trade-offs. They make excellent blog posts and interview stories.

## Distributed systems
- [ ] **O1 Mini-Temporal**: workflows *as code* in Go with deterministic replay (record side effects; replay from history). Compare it with your JSON-DSL engine
- [ ] **O2 Kafka as the source of truth**: move run history from Postgres to Kafka (compacted + event topics). Prototype it and argue whether it's better
- [ ] **O3 Distributed cron**: leader election via etcd leases; exactly-once firing across 3 replicas; clock skew tests
- [ ] **O4 Consistent hashing**: a ring with virtual nodes + bounded loads; simulate node joins/failures; plot key movement and load variance
- [ ] **O5 Raft KV (MIT Lab 4)** + linearizability checking with **Porcupine**
- [ ] **O6 CRDTs**: G-counter, PN-counter, OR-set, then a collaborative workflow editor over WebSockets
- [ ] **O7 Multi-region Orbit**: active-active control plane, home-region runs, failover drills (on paper + a 2-region local simulation)
- [ ] **O8 Exactly-once metering**: billing-grade usage counting from Kafka to ClickHouse to invoices; prove there's no double counting

## Storage & performance
- [ ] **O9 LSM engine in Go**: memtable, WAL, SSTables, compaction, bloom filters; benchmark against bbolt (B+tree)
- [ ] **O10 Java vs Go honest comparison**: reimplement the LLM gateway in Java (virtual threads) and compare throughput, p99, memory, startup, and dev time
- [ ] **O11 GraalVM native image** for orbit-api: startup, RSS, and throughput trade-offs; what broke?
- [ ] **O12 Bloom filter + count-min sketch** for webhook dedupe and top-K tenants by traffic

## Infra & platform
- [ ] **O13 A mini service mesh sidecar** in Go: a TCP/HTTP proxy with mTLS (your own CA), retries, and metrics
- [ ] **O14 Custom K8s scheduler plugin** placing "GPU-ish" workers by a custom resource
- [ ] **O15 WASM plugin system** for custom tools (wazero in Go): isolation, limits, and a host API
- [ ] **O16 Zanzibar-style authz** with OpenFGA: workflow sharing between users/teams/tenants
- [ ] **O17 Reproduce a famous outage**: a retry storm, a cache stampede, or a metastable failure, in your lab. Write the post-mortem

## AI
- [ ] **O18 Fine-tune vs prompt**: a LoRA fine-tune of a small open model for UC1 classification vs few-shot prompting vs a cascade. Compare accuracy, cost, and latency
- [ ] **O19 Semantic cache research**: choose embedding model + threshold; measure precision/recall of cache hits on paraphrase sets
- [ ] **O20 Agent that builds its own tools**: generates a tool, tests it in the sandbox, registers it after approval. What guardrails are needed?
- [ ] **O21 Multi-agent debate vs single agent**: eval study on 50 reasoning tasks
- [ ] **O22 Voice agent**: a realtime speech pipeline (STT → LLM → TTS) with barge-in; measure end-to-end latency
- [ ] **O23 GraphRAG vs hybrid RAG** on a multi-hop question set
- [ ] **O24 Eval-driven prompt optimization**: automatic prompt search with your eval suite as the objective

## Community
- [ ] **O25 A merged open-source PR** to something you used: Spring AI, an MCP SDK, LangGraph, franz-go, pgx, KEDA, or Envoy Gateway
