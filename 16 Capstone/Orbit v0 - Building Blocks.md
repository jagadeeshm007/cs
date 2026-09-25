---
tags: [capstone, orbit]
version: v0
weeks: W1–W4
---
# Orbit v0: Building Blocks (Phase 1)

Small, sharp components you will later embed in Orbit. **Build from scratch, no frameworks.**

- [ ] **`orbit-kv` (Java)**: thread-safe KV with TTL + LRU, RESP-like TCP protocol on virtual threads → later becomes the idea behind the gateway's cache
- [ ] **`orbit-ratelimit` (Java + Go)**: token bucket, sliding-window log, and sliding-window counter; identical test vectors in both languages
- [ ] **`orbit-dag` (Go)**: in-memory DAG executor: JSON workflow → topo sort (Kahn) → bounded-parallel execution, per-step timeout, retries with exponential backoff + jitter, cancel-on-failure with `context` → **the seed of orbit-engine**
- [ ] **`orbit-expr` (Go)**: tiny expression language (lexer + Pratt parser + evaluator) for step conditions like `steps.a.output.score > 0.8 && input.tier == "pro"` (*Writing an Interpreter in Go* ch. 1–3)
- [ ] **Mini Redis (Go)**: CodeCrafters/codingchallenges stages
- [ ] **LLD rounds** modeled on Orbit: design the class model for `Workflow`, `Step`, `Run`, `StepExecutor` (Strategy), `RetryPolicy`, `StepState` (State pattern)

## Definition of done
- [ ] All race-detector / concurrency tests green · [ ] Benchmarks (JMH, `go test -bench`) committed · [ ] README per module · [ ] ADR-000: "Why Java for the control plane and Go for the data plane"
