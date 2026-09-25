---
tags: [roadmap, timeline]
start: 2026-09-28
end: 2027-03-28
---
# 📅 Master Timeline (24 weeks + 2 buffer)

> [!info] Six lanes every week
> **🧩 DSA** (Java, 2h/day) · **📖 Core** (books/courses) · **⚙️ Internals** (how it works underneath) · **🎯 Assignment** (graded, builds Orbit) · **🔬 Lab** (MIT-style) · **🧠 Cognitive** (thinking drill) + a Saturday **🧩 pattern kata**
> Full assignment specs: `Assignments - Phase N` · Labs: [[Labs Index]] · Grade yourself with the [[Grading Rubric]] · Weekly review every Sunday

---
## Phase 1: Foundations (W1–W4) → [[Phase 1 - Foundations]] · builds [[Orbit v0 - Building Blocks]]

### W1 · 28 Sep – 4 Oct
- [ ] 🛠️ Setup: JDK 25, Go 1.25+, IDEs, Docker, Git/GitHub, Anki, LeetCode, Ollama · fill in the [[Skill Matrix]]
- [ ] 🧩 DSA: complexity, Java collections, **arrays & hashing** (15)
- [ ] 📖 Core: [[Java Advanced]] (modern Java, collections) · [[Operating Systems]]
- [ ] ⚙️ Internals: [[JVM Internals]] §1–3, §8 · [[Linux & OS Internals]]
- [ ] 🎯 **A1 Concurrent KV store (Java)** → [[Assignments - Phase 1]]
- [ ] 🔬 Lab: JOL memory layouts
- [ ] 🧩 Kata: Strategy + Factory · SOLID
- [ ] 🧠 Cognitive: Predict → verify lock-striping throughput

### W2 · 5 – 11 Oct
- [ ] 🧩 DSA: **two pointers, sliding window, prefix sums** (18)
- [ ] 📖 Core: [[Concurrency]] · virtual threads · *JCIP* ch. 1–5
- [ ] ⚙️ Internals: [[JVM Internals]] §4–7 (GC, JMM, AQS, Loom)
- [ ] 🎯 **A2 Thread pool + rate limiters (Java)**
- [ ] 🔬 Lab: racy counter → `synchronized` / `AtomicLong` / `LongAdder` under JMH
- [ ] 🧩 Kata: Builder (+ Go functional options) + Observer
- [ ] 🧠 Cognitive: Feynman teach-back on happens-before

### W3 · 12 – 18 Oct
- [ ] 🧩 DSA: **stack, monotonic stack, binary search on answer** (18)
- [ ] 📖 Core: [[Go Advanced]] · *Learning Go* · *Concurrency in Go* · [[Networking]]
- [ ] ⚙️ Internals: [[Go Runtime Internals]] · [[Network Stack Internals]] §1–3
- [ ] 🎯 **A3 DAG executor + `orbit-expr` (Go)**
- [ ] 🔬 Lab: `schedtrace` + escape analysis; *Writing an Interpreter in Go* ch. 1–3
- [ ] 🧩 Kata: Decorator (Go middleware) + Adapter
- [ ] 🧠 Cognitive: predict heap escapes

### W4 · 19 – 25 Oct
- [ ] 🧩 DSA: **linked list, recursion** (15) + first **weekly contest**
- [ ] 📖 Core: [[Database Internals]] · [[Python Essentials]] · [[Low-Level Design & Machine Coding]]
- [ ] ⚙️ Internals: [[PostgreSQL Internals]] §1–3 (MVCC)
- [ ] 🎯 **A4 Mini Redis (Go) + 2 LLD rounds + isolation anomalies**
- [ ] ⚫ **Boss fight: 1BRC in Java + Go**
- [ ] 🧩 Kata: State + Command + Template Method
- [ ] 🧠 Cognitive: blank-page "type a URL" answer · 🔁 Phase 1 retro

---
## Phase 2: Backend + first AI (W5–W9) → [[Phase 2 - Backend Engineering]] · builds [[Orbit v1 - Core Platform]]

### W5 · 26 Oct – 1 Nov
- [ ] 🧩 DSA: **trees** (18)
- [ ] 📖 Core: [[Spring Core & Boot]] · [[Docker]] (compose)
- [ ] ⚙️ Internals: [[Spring Internals]] §1–4
- [ ] 🎯 **A5 orbit-api skeleton** → [[Assignments - Phase 2]]
- [ ] 🔬 Lab (🔴): **mini DI container** with proxies
- [ ] 🧩 Kata: Proxy + Chain of Responsibility
- [ ] 🧠 Cognitive: draw `refresh()` from memory

### W6 · 2 – 8 Nov
- [ ] 🧩 DSA: **BST, heaps, top-K** (15)
- [ ] 📖 Core: [[PostgreSQL]] · [[Spring Data & JPA]] · [[LLM Fundamentals]] (intro: API calls, structured output)
- [ ] ⚙️ Internals: [[PostgreSQL Internals]] §4–7 · [[Spring Internals]] §7
- [ ] 🎯 **A6 data layer + LLM gateway v0 (Go) + UC1 v0 structured classification**
- [ ] 🔬 Lab: 5M-row EXPLAIN tuning
- [ ] 🧩 Kata: Repository + Unit of Work + Specification
- [ ] 🧠 Cognitive: predict query plans

### W7 · 9 – 15 Nov
- [ ] 🧩 DSA: **backtracking** (15)
- [ ] 📖 Core: [[Spring Security]] · [[REST API Design]] · [[Security Engineering]] (AppSec part)
- [ ] ⚙️ Internals: [[Spring Internals]] §5–6
- [ ] 🎯 **A7 multi-tenancy: Keycloak, API keys, RLS, idempotency starter**
- [ ] 🔬 Lab: PortSwigger access control + JWT (≥ 6 labs)
- [ ] 🧩 Kata: Composite + Visitor → sealed interfaces
- [ ] 🧠 Cognitive: draw PKCE from memory; STRIDE on API keys

### W8 · 16 – 22 Nov
- [ ] 🧩 DSA: **graphs I** (15)
- [ ] 📖 Core: [[Go Backend Development]] · [[Redis]] · [[gRPC & Protobuf]] · [[Frontend Essentials]] (4h)
- [ ] ⚙️ Internals: [[Redis Internals]] · [[Network Stack Internals]] §4–5
- [ ] 🎯 **A8 tool-calling loop from scratch + gRPC + Lua quotas + UC1 v1**
- [ ] 🔬 Lab: mini Redis replication/RDB · Wireshark gRPC
- [ ] 🧩 Kata: Interpreter + Memento
- [ ] 🧠 Cognitive: pre-mortem of the tool loop

### W9 · 23 – 29 Nov
- [ ] 🧩 DSA: **graphs II**: topo sort, union-find, Dijkstra (15)
- [ ] 📖 Core: [[GraphQL]] · [[Realtime (WebSockets, SSE)]] · React (4h)
- [ ] 🎯 **A9 streaming + GraphQL + UI + UC2 v0 → ship Orbit v1**
- [ ] ⚫ **Boss fight: 200 streaming chats + 50 runs/s, fix 2 bottlenecks**
- [ ] 🧩 Kata: Ports & Adapters + Anti-corruption layer
- [ ] 🧠 Cognitive: self-review your W5 ADRs · 🔁 Phase 2 retro + blog post

---
## Phase 3: Distributed Systems (W10–W14) → [[Phase 3 - Distributed Systems & System Design]] · builds [[Orbit v2 - Durable Workflows]]

### W10 · 30 Nov – 6 Dec
- [ ] 🧩 DSA: **DP I** (15)
- [ ] 📖 Core: DDIA ch. 5–9 · [[Distributed Systems]] · [[System Design Roadmap]] · [[Estimation Cheatsheet]]
- [ ] 🎯 **A10 durable execution: event history, leases, fencing** → [[Assignments - Phase 3]]
- [ ] 🔬 Lab: **MIT 6.5840 Lab 1 MapReduce**
- [ ] 🧩 Kata: Lease + Fencing token + Idempotent receiver
- [ ] 🧠 Cognitive: first-principles fencing interleaving · 🏛️ Cases: URL shortener, rate limiter

### W11 · 7 – 13 Dec
- [ ] 🧩 DSA: **DP II** (15)
- [ ] 📖 Core: [[Kafka]] · [[Architecture Patterns]]
- [ ] ⚙️ Internals: [[Kafka Internals]]
- [ ] 🎯 **A11 outbox + Kafka + orbit-hooks (triggers, webhooks, DLQ) + UC9**
- [ ] 🔬 Lab: **Gossip Glomers 1–3**
- [ ] 🧩 Kata: Outbox + Inbox + Competing consumers
- [ ] 🧠 Cognitive: predict ordering under rebalance · 🏛️ Cases: notification system, news feed

### W12 · 14 – 20 Dec
- [ ] 🧩 DSA: **DP III** (12)
- [ ] 📖 Core: [[Spring Cloud & Microservices]] · *Microservices Patterns* (sagas)
- [ ] 🎯 **A12 HITL + sagas + versioning + circuit breakers + UC3 refund agent**
- [ ] 🔬 Lab: **MIT 6.5840 Lab 2** · a Temporal sample
- [ ] 🧩 Kata: Saga + Compensating transaction + Process manager
- [ ] 🧠 Cognitive: pre-mortem of UC3 · 🏛️ Cases: chat system, payment system

### W13 · 21 – 27 Dec
- [ ] 🧩 DSA: **greedy + intervals** (15)
- [ ] 📖 Core: Raft paper · [[Search & Other Stores]]
- [ ] 🎯 **A13 fair scheduling + admission control + run search (CQRS)**
- [ ] 🔬 Lab (⚫): **MIT 6.5840 Lab 3A–3B Raft**
- [ ] 🧩 Kata: Leader election + Scheduler-agent-supervisor
- [ ] 🧠 Cognitive: Raft teach-back · 🏛️ Cases: distributed cache, KV store, job scheduler

### W14 · 28 Dec – 3 Jan
- [ ] 🧩 DSA: **tries, bits, math** + revise `#revise`
- [ ] 🎯 **A14 ship Orbit v2**
- [ ] ⚫ **Boss fight: Chaos Day (5,000 runs, 0 lost, 0 duplicates) + post-mortem**
- [ ] 🔬 Lab: Gossip Glomers 4–5
- [ ] 🧩 Kata: CQRS + Materialized view + Event sourcing
- [ ] 🧠 Cognitive: constraint flip to 1M runs/s · 🏛️ Mock: "Design a workflow engine" · 🔁 Phase 3 retro

---
## Phase 4: Cloud Native, Ops & Data (W15–W18) → [[Phase 4 - Cloud Native, Ops & Data]] · builds [[Orbit v3 - Cloud Native]]

### W15 · 4 – 10 Jan
- [ ] 🧩 DSA: **advanced graphs** + segment tree/BIT
- [ ] 📖 Core: [[Docker]] deep · [[Kubernetes]]
- [ ] ⚙️ Internals: [[Container Internals]] · [[Kubernetes Internals]]
- [ ] 🎯 **A15 Helm + KEDA + graceful leases + `OrbitWorkerPool` operator** → [[Assignments - Phase 4]]
- [ ] 🔬 Lab: Kubernetes the Hard Way
- [ ] 🧩 Kata: Sidecar + Ambassador + Operator
- [ ] 🧠 Cognitive: trace `kubectl apply` · 📨 **Start applying** ([[Resume & Applications]])

### W16 · 11 – 17 Jan
- [ ] 🧩 DSA: **DP IV**: bitmask/tree DP (10)
- [ ] 📖 Core: [[Envoy, Gateways & Service Mesh]] · [[Cloud (AWS)]] · [[Terraform & IaC]]
- [ ] ⚙️ Internals: [[Envoy Internals]]
- [ ] 🎯 **A16 Envoy Gateway + ext_authz (Go) + gVisor code sandbox + Terraform**
- [ ] 🔬 Lab: **containers from scratch in Go**
- [ ] 🧩 Kata: Gateway offloading + Valet key + Claim check
- [ ] 🧠 Cognitive: predict which timeout breaks the stream

### W17 · 18 – 24 Jan
- [ ] 🧩 DSA: company-tagged mediums (20)
- [ ] 📖 Core: [[CI-CD & GitOps]] · [[Observability]]
- [ ] 🎯 **A17 OTel (GenAI spans) + SLOs + ArgoCD + canary auto-rollback**
- [ ] 🔬 Lab (🔴): **mini tracer in Go** (W3C propagation over HTTP + Kafka)
- [ ] 🧩 Kata: Queue-based load leveling + Throttling + Bulkhead
- [ ] 🧠 Cognitive: symptom → hypotheses from dashboards only

### W18 · 25 – 31 Jan
- [ ] 🧩 DSA: mixed revision + 2 contests
- [ ] 📖 Core: [[SRE & Reliability]] · [[Security Engineering]] · [[Data Pipelines]]
- [ ] 🎯 **A18 ingestion pipeline + ClickHouse analytics + threat model**
- [ ] ⚫ **Boss fight: Production Day (cloud, 1-hour soak, 3 failures, < $10)**
- [ ] 🔬 Lab: windowed stream aggregation (Flink SQL / Kafka Streams)
- [ ] 🧩 Kata: Pipes & filters + Deployment stamps/cells
- [ ] 🧠 Cognitive: Fermi on infra + LLM cost · 🔁 Phase 4 retro

---
## Phase 5: AI Engineering (W19–W22) → [[Phase 5 - AI Engineering]] · builds [[Orbit v4 - Agents, RAG & MCP]]

### W19 · 1 – 7 Feb
- [ ] 🧩 DSA: maintenance (1.5h/day)
- [ ] 📖 Core: [[LLM Fundamentals]] · [[Spring AI]] · *AI Engineering* (Huyen)
- [ ] ⚙️ Internals: [[LLM Inference Internals]]
- [ ] 🎯 **A19 gateway v2 (routing, cascade, prompt + semantic cache, budgets) + UC5 + UC8** → [[Assignments - Phase 5]]
- [ ] 🔬 Lab (🔴): minbpe; TTFT/prompt-caching measurements
- [ ] 🧩 Kata: Prompt chaining + Routing + Model cascade
- [ ] 🧠 Cognitive: predict tokens and cost

### W20 · 8 – 14 Feb
- [ ] 📖 Core: [[RAG]]
- [ ] 🎯 **A20 hybrid RAG + rerank + ACLs + eval set → UC2 full**
- [ ] 🔬 Lab (🔴): **BM25 + HNSW from scratch in Go**
- [ ] 🧩 Kata: RAG variants + Reranking + Semantic cache
- [ ] 🧠 Cognitive: error analysis of 30 failures

### W21 · 15 – 21 Feb
- [ ] 📖 Core: [[Agents & Workflows]] · [[LangChain & LangGraph]] · [[MCP]]
- [ ] 🎯 **A21 ReAct agent from scratch (Go) + LangGraph + Orbit MCP server/client + UC4, UC10, UC11**
- [ ] 🔬 Lab: LangChain Academy LangGraph modules 1–5
- [ ] 🧩 Kata: ReAct + Plan-and-execute + Orchestrator–workers + Supervisor
- [ ] 🧠 Cognitive: "What did the framework hide?"

### W22 · 22 – 28 Feb
- [ ] 📖 Core: [[Evals, Guardrails & LLMOps]]
- [ ] 🎯 **A22 evals CI gate + guardrails + UC6 text-to-SQL + UC7 SRE agent + UC12**
- [ ] ⚫ **Boss fight: Red-Team Day (30+ attacks)**
- [ ] 🧩 Kata: Evaluator–optimizer + Guardrail sandwich + Dual LLM + HITL
- [ ] 🧠 Cognitive: transfer classic security → agent security · 🔁 Phase 5 retro

---
## Phase 6: Interview Mode (W23–W26) → [[Phase 6 - Interview Mode]] · builds [[Orbit v5 - Scale & Polish]]

### W23 · 1 – 7 Mar
- [ ] 🎯 **A23 scale + cost** → [[Assignments - Phase 6]]
- [ ] Mocks: 2 DSA · 2 HLD (incl. "Design an AI workflow platform") · 1 LLD · behavioral stories final
- [ ] ⚙️ Internals revision: 3 notes/day, interview questions only

### W24 · 8 – 14 Mar
- [ ] 🎯 **A24 portfolio + interview transfer**
- [ ] Company-specific prep ([[Interview Strategy]]); revise all `#revise` + `#interview-q`
- [ ] Final Skill Matrix

### W25–W26 · 15 – 28 Mar: Buffer
- [ ] Pick 2 from [[Open Assignments]] · keep 1 contest + 2 mocks per week while interviewing
