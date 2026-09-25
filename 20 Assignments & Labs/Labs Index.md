---
tags: [assignments, labs, moc]
---
# 🔬 Labs Index: external + custom (progressive)

Difficulty: 🟢 warm-up · 🟡 core · 🔴 hard · ⚫ boss. Status: `[ ]` / `[/]` / `[x]`

## External, world-class labs
| Lab | Lang | Week | Diff | What you learn |
|---|---|---|---|---|
| [ ] **1 Billion Row Challenge (1BRC)** | Java + Go | W4 | 🔴 | Parsing, memory, SIMD-ish tricks, parallelism, profiling |
| [ ] **Build your own Redis** (CodeCrafters / codingchallenges.fyi) | Go | W3–W8 | 🟡 | TCP, RESP, concurrency, expiry, replication |
| [ ] **Writing an Interpreter in Go** (Thorsten Ball) ch. 1–4 | Go | W3–W8 | 🟡 | Lexer, Pratt parser, evaluator → `orbit-expr` |
| [ ] **Build Your Own Database From Scratch in Go** (build-your-own.org) | Go | W4–W6 | 🔴 | B+tree, KV, transactions |
| [ ] **MIT 6.5840 Lab 1: MapReduce** | Go | W10 | 🟡 | Coordination, fault tolerance |
| [ ] **MIT 6.5840 Lab 2: KV server** | Go | W12 | 🟡 | Linearizability over lossy networks |
| [ ] **MIT 6.5840 Lab 3A–3D: Raft** | Go | W13–W14 | ⚫ | Consensus, the hardest and best |
| [ ] MIT 6.5840 Lab 4: Fault-tolerant KV on Raft | Go | W25+ | ⚫ | Replicated state machines |
| [ ] **Fly.io Gossip Glomers** (all 6) | Go | W11–W14 | 🟡→🔴 | Broadcast, CRDT counters, Kafka log, transactions |
| [ ] **PingCAP TinyKV** (Talent Plan) | Go | Open | ⚫ | Raft KV + Percolator transactions |
| [ ] **Kubernetes the Hard Way** | — | W15 | 🔴 | Every control-plane component |
| [ ] **Containers from scratch** (Liz Rice) | Go | W16 | 🟡 | Namespaces, cgroups |
| [ ] **kubebuilder tutorial → your own operator** | Go | W15 | 🔴 | Controllers, CRDs |
| [ ] **PortSwigger Web Security Academy** (access control, JWT, SSRF, SQLi) | — | W7, W18 | 🟡 | AppSec |
| [ ] **pgexercises.com** | SQL | W6 | 🟢 | SQL fluency |
| [ ] **LangChain Academy: Intro to LangGraph** | Python | W21 | 🟡 | Agents, persistence, HITL |
| [ ] **Karpathy: minbpe / Let's build GPT** | Python | W19 | 🔴 | Tokenizers, transformers |
| [ ] DataTalksClub DE Zoomcamp (streaming module) | — | W18 | 🟡 | Stream processing |

## Custom labs (in the `Assignments - Phase N` notes)
| Lab | Week | Diff |
|---|---|---|
| [ ] Concurrent KV with TTL/LRU + RESP protocol (Java) | W1 | 🟡 |
| [ ] Thread pool + rate limiters from scratch (Java) | W2 | 🟡 |
| [ ] DAG executor with retries/cancellation (Go) | W3 | 🟡 |
| [ ] Mini DI container with proxies (Java) | W5 | 🔴 |
| [ ] LLM gateway with streaming + Lua quotas (Go) | W6–W8 | 🔴 |
| [ ] Tool-calling loop from scratch (Go) | W8 | 🟡 |
| [ ] Durable execution engine with leases + fencing (Go) | W10–W12 | ⚫ |
| [ ] Outbox + webhook dispatcher with DLQ (Go) | W11 | 🟡 |
| [ ] Weighted fair scheduler across tenants (Go) | W13 | 🔴 |
| [ ] ext_authz server for Envoy (Go) | W16 | 🟡 |
| [ ] Mini tracer with W3C context propagation over HTTP + Kafka (Go) | W17 | 🔴 |
| [ ] Ingestion pipeline (pipes & filters) with idempotent resume | W18 | 🔴 |
| [ ] BM25 + simplified HNSW from scratch (Go) | W20 | 🔴 |
| [ ] ReAct agent from scratch (Go) | W21 | 🟡 |
| [ ] Red-team suite for your own agents | W22 | 🔴 |
