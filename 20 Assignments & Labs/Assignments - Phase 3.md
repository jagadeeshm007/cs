---
tags: [assignments, phase-3]
weeks: W10–W14
---
# 📝 Assignments: Phase 3 (Distributed Systems: the durable engine)

## W10 - Durable Execution v1 (Go) 🔴
**🎯 A10** Turn `orbit-dag` into `orbit-engine` ([[Orbit v2 - Durable Workflows]])
- [ ] An append-only `run_events` table; run state = **replay(events)**; snapshots every N events
- [ ] Task queue: `SELECT … FOR UPDATE SKIP LOCKED LIMIT n`; **leases** (`leased_until`) + heartbeats; expired leases are re-queued
- [ ] **Fencing token** = lease epoch; `CompleteTask(taskId, epoch)` is rejected if the epoch is stale
- [ ] Idempotency key per step attempt passed to tools; an idempotent sink to verify effects
- **Acceptance (chaos test):** 1,000 runs × 5 steps while a script `kill -9`s random workers every 2 s and `SIGSTOP`s one for 30 s (a "GC pause") → **all runs complete, 0 duplicate effects, 0 stale completions accepted**

**🔬 Lab:** MIT 6.5840 **Lab 1 MapReduce**
**🧠 Cognitive:** *First-principles*: write the exact interleaving where a paused worker corrupts state without fencing, then show how the epoch prevents it
**🌀 Open:** Postgres queue vs Kafka vs Redis Streams for task dispatch at 100 / 10k / 1M tasks/s: where does each break?
**Score:** __/28

## W11 - Kafka Backbone, Triggers & Webhooks
**🎯 A11**
- [ ] **Transactional outbox** in orbit-api + engine → Debezium (or a Go relay) → `run.events`, `usage.events` (Protobuf + Schema Registry, key = runId/tenantId)
- [ ] **orbit-hooks (Go)**: inbound webhooks (HMAC verification, dedupe by delivery ID), cron triggers (next-fire index), Kafka-topic triggers → `StartRun`
- [ ] Outbound webhooks: HMAC signatures, exponential backoff, retry topics (1m/10m/1h), **DLQ** + replay CLI
- [ ] **UC9**: meeting transcript webhook → summarize → extract action items (schema) → create tasks via tool → idempotent on redelivery
- **Acceptance:** send each inbound webhook 3× → exactly 1 run; kill the relay mid-stream → no lost events

**🔬 Lab:** **Gossip Glomers** 1–3 (echo, unique IDs, broadcast 3a–3e) ([[Kafka Internals]] for the log challenge later)
**🧠 Cognitive:** *Predict*: ordering guarantees for keyed events across 6 partitions during a consumer rebalance → verify with an experiment
**🌀 Open:** Choreography vs orchestration for Orbit's internal flows (billing, notifications, search indexing)
**Score:** __/28

## W12 - Sagas, HITL, Versioning & Resilience
**🎯 A12**
- [ ] `human` step: approval inbox API, signals, **timeout → escalate** timers
- [ ] Compensation handlers + reverse-order compensation on failure
- [ ] **UC3 refund agent**: lookup order (tool) → policy check → propose a refund → approval → payment tool (idempotent) → notify; on a payment failure → compensate
- [ ] **Workflow versioning**: in-flight runs stay on v1 while v2 publishes; a migration policy for long waits
- [ ] Circuit breakers per LLM provider (gobreaker) + fallback provider; bulkheads per step type
- **Acceptance:** 100 UC3 runs with random worker kills + a 20% payment tool failure rate → 0 double refunds; every refund has an audit trail

**🔬 Lab:** MIT 6.5840 **Lab 2 (KV server)**; run one sample in **Temporal** (Go SDK)
**🧠 Cognitive:** *Pre-mortem* of UC3; map each failure to its compensation
**🌀 Open:** ADR: "Our engine vs Temporal": when would you migrate? What do you lose and gain?
**Score:** __/28

## W13 - Raft & Multi-Tenant Fairness
**🎯 A13**
- [ ] Per-tenant queues + **weighted fair scheduling** (deficit round robin) + per-tenant concurrency caps + priority tiers
- [ ] Admission control: 429 + `Retry-After` when a tenant's backlog exceeds its quota
- [ ] Run search: OpenSearch projection from `run.events` (CQRS), rebuildable from scratch
- **Acceptance:** tenant A floods 100k runs; tenants B–E (100 runs each) finish with p95 queue wait < 2 s

**🔬 Lab (⚫):** MIT 6.5840 **Lab 3A** (leader election) + **3B** (log replication)
**🧠 Cognitive:** *Feynman*: explain Raft election safety + log matching in 5 minutes
**🌀 Open:** Noisy neighbors at 10,000 tenants: shared pools vs cells vs dedicated workers for enterprise tiers
**Score:** __/28

## W14 - v2 Ship & Chaos Day
**🎯 A14** Ship [[Orbit v2 - Durable Workflows]]: ADRs, sequence diagrams (happy, retry, lease expiry, compensation), README update
**🔬 Lab:** Gossip Glomers 4 (grow-only counter) + 5 (Kafka-style log); Raft 3C if you have time

**⚫ Phase boss fight: Chaos Day.** 5,000 runs across UC1/UC3/UC9 while randomly: killing engine and worker pods, restarting a Kafka broker, failing over Postgres, injecting 2 s of latency into the LLM mock (toxiproxy)
- **Acceptance:** 0 lost runs, 0 duplicate side effects, all SLO breaches explained. Write it as a **post-mortem** (timeline, impact, root causes, action items)

**🧠 Cognitive:** *Constraint flip*: redesign the engine for 1M runs/s. What changes first?
**Score:** __/28
