---
tags: [patterns, anti-patterns]
---
# 🚫 Anti-Patterns & Code Smells

## Code level
God class · long method · feature envy · primitive obsession (use value objects: `TenantId`, `Money`) · shotgun surgery · long parameter lists · boolean flag parameters · magic numbers · deep inheritance · swallowed exceptions · `null` returns instead of `Optional`/errors · Go: ignoring errors, huge interfaces, `interface{}` everywhere, goroutines without an owner or cancellation

## Service & data level
| Anti-pattern | Why it hurts | Fix |
|---|---|---|
| **Distributed monolith** | Services must deploy together | Real boundaries, async contracts |
| **Shared database across services** | Coupling, hidden contracts | DB per service + events/APIs |
| **Dual writes** (DB + Kafka separately) | Inconsistency on partial failure | Outbox / CDC |
| **Chatty services / sync call chains** | Latency and availability multiply | Aggregate, async, cache |
| **No timeouts** | Thread/connection exhaustion | Timeouts everywhere + deadlines |
| **Retries without backoff or budget** | Retry storms | Exponential backoff + jitter + budgets |
| **Unbounded queues** | Memory blowups, latency | Bounded + backpressure + shedding |
| **Cache without TTL / invalidation plan** | Stale data forever | TTL + events + versioned keys |
| **N+1 queries** | DB overload | Batch/join fetch, DataLoader |
| **Premature microservices** | Complexity without benefit | Modular monolith first |
| **Big-bang rewrite** | Risk | Strangler fig |
| **Logging secrets/PII** | Breaches | Redaction, structured logging policy |
| **Golden hammer** | "Kafka for everything" | Choose per requirement |

## AI-specific
| Anti-pattern | Fix |
|---|---|
| Agent for a task a fixed workflow could do | Start with a workflow pattern |
| No evals ("vibes-based" prompting) | A golden dataset + CI gate |
| Mega-prompt with everything stuffed in | Retrieval, routing, compaction |
| Trusting tool output / retrieved docs as instructions | Treat as data; dual LLM; scoped tools |
| Unbounded agent loops | Step/token/$ budgets, loop detection |
| Letting the LLM execute side effects without confirmation | HITL for irreversible actions |
| Non-idempotent tools under retries | Idempotency keys |
| No cost attribution | Per-tenant/per-workflow token accounting |
| Changing the embedding model without re-indexing | Versioned indexes + backfill |

## 🧠 Drill
Every Sunday, pick one file in Orbit and hunt for 3 smells. Refactor one. Log it in the Weekly Review.
