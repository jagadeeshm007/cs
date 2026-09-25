---
tags: [capstone, orbit]
version: v2
weeks: W10–W14
---
# Orbit v2: Durable Workflow Engine (Phase 3)

## Scope
- [ ] **Event-sourced run history**: `RunStarted`, `StepScheduled`, `StepStarted`, `StepCompleted`, `StepFailed`, `TimerStarted`, `TimerFired`, `SignalReceived`, `RunCompleted`; run state = fold(history)
- [ ] **Task queue with leases**: Postgres `SELECT … FOR UPDATE SKIP LOCKED`, lease expiry + heartbeats, **fencing tokens** (lease epoch) checked on completion
- [ ] **Exactly-once effects**: idempotency key = `runId/stepId/attempt`, passed to tools; dedupe table (inbox)
- [ ] **Timers**: `wait` step, retry backoff timers, approval timeouts (indexed `fire_at` + poller; compare with Redis ZSET)
- [ ] **HITL**: `human` step → approvals inbox → signal API → resume; escalate on timeout
- [ ] **Sagas**: per-step compensation handlers; reverse-order compensation on failure
- [ ] **Workflow versioning**: runs pinned to a definition version; safe deploys
- [ ] **Kafka backbone**: transactional outbox → Debezium/relay → `run.events`, `usage.events` (Protobuf + Schema Registry)
- [ ] **orbit-hooks (Go)**: cron triggers, inbound webhooks (signature verification, dedupe), Kafka triggers; outbound webhooks (HMAC, retries, retry topics, DLQ)
- [ ] **Fairness**: per-tenant concurrency caps + weighted round-robin across tenant queues; 429 + `Retry-After` admission control
- [ ] **Resilience**: circuit breakers per LLM provider; bulkheads per step type
- [ ] **Run search**: OpenSearch projection from Kafka (CQRS)
- [ ] Compare against **Temporal**: port UC3 to Temporal (Go SDK) and write the ADR

## Use cases shipped
UC3 Refund agent with approvals + compensation · UC9 Meeting notes → actions

## Definition of done
- [ ] **Chaos gate**: 5,000 runs while randomly `kill -9`-ing engine/workers, restarting a Kafka broker, and failing Postgres over → **0 lost runs, 0 duplicate side effects** (verified by an idempotent sink)
- [ ] Sequence diagrams for the happy path, retry, lease-expiry, and compensation
- [ ] Blog: "Building durable execution from scratch in Go"
