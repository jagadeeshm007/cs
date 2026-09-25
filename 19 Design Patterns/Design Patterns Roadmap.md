---
tags: [patterns, moc]
---
# 🧩 Design Patterns Roadmap: code → service → system → AI

> [!important] How patterns actually make you better
> Patterns are a **vocabulary for trade-offs**, not templates to paste. For each one, learn: the **problem** (forces), the **structure**, **where it already exists** in Spring/Go stdlib/Kafka/K8s, **when NOT to use it**, and **implement it once in Java and once in Go**.

## The pattern ladder
| Level | Note | Weeks |
|---|---|---|
| 1. Object design (GoF + SOLID) | [[GoF Patterns (Java & Go)]] | W1–W4 |
| 2. Concurrency | [[Concurrency Patterns]] | W2–W3, revisit W10 |
| 3. Application & domain | [[Enterprise & DDD Patterns]] | W5–W9 |
| 4. Distributed & cloud | [[Distributed & Cloud Patterns]] | W10–W18 |
| 5. AI & agents | [[AI & Agent Patterns]] | W19–W22 |
| Always | [[Anti-Patterns & Code Smells]] | every code review |

## Weekly pattern kata (every Saturday, 90 min)
1. Pick 2 patterns from this week's list
2. Implement each in **Java and Go** (≤ 60 lines each), with a test
3. **Find it in the wild**: locate the pattern in Spring/JDK/Go stdlib/Kubernetes source and link the file in your note
4. **Apply it to Orbit** (or explain why it doesn't fit)
5. Write "**When NOT to use**" in 3 bullets
6. Log it in the table below

| Week | Patterns | Found in the wild | Orbit usage | Done |
|---|---|---|---|---|
| W1 | Strategy, Factory | `Comparator`, `BeanFactory` | LLM provider adapters | [ ] |
| W2 | Builder (+ Go functional options), Observer | `RestClient.builder()`, `ApplicationListener` | Workflow builder, run events | [ ] |
| W3 | Decorator (Go middleware), Adapter | `http.Handler` chains, `HandlerAdapter` | Gateway middleware | [ ] |
| W4 | State, Command, Template Method | `Thread.State`, `Runnable`, `JdbcTemplate` | Step state machine, step commands | [ ] |
| W5 | Proxy, Chain of Responsibility | Spring AOP, `FilterChainProxy` | Tool auth chain | [ ] |
| W6 | Repository, Unit of Work, Specification | Spring Data, Hibernate Session | Workflow repo | [ ] |
| W7 | Composite, Visitor → sealed + pattern matching | ASTs, `FileVisitor` | Workflow DAG, expression AST | [ ] |
| W8 | Interpreter, Memento | SpEL | `orbit-expr`, run checkpoints | [ ] |
| W9 | Ports & Adapters, Anti-corruption layer | — | Provider/tool integrations | [ ] |
| W10 | Lease, Fencing token, Idempotent receiver | etcd leases, Kafka producer IDs | Task leasing | [ ] |
| W11 | Outbox, Inbox, Competing consumers | Debezium | Event backbone | [ ] |
| W12 | Saga, Compensating transaction, Process manager | Temporal | UC3 refunds | [ ] |
| W13 | Leader election, Scheduler-agent-supervisor | K8s leader election | Engine timers | [ ] |
| W14 | CQRS, Materialized view, Event sourcing | — | Run history, search | [ ] |
| W15 | Sidecar, Ambassador, Operator | Envoy, controllers | Worker pool operator | [ ] |
| W16 | Gateway offloading, Valet key, Claim check | Envoy, S3 presigned URLs | Uploads, large payloads | [ ] |
| W17 | Queue-based load leveling, Throttling, Bulkhead | KEDA, resilience4j | Workers, per-tenant caps | [ ] |
| W18 | Pipes & filters, Deployment stamps/cells | Unix pipes | Ingestion pipeline | [ ] |
| W19 | Prompt chaining, Routing, Model cascade | — | UC1, UC8, gateway | [ ] |
| W20 | RAG variants, Reranking, Semantic cache | — | UC2 | [ ] |
| W21 | ReAct, Plan-and-execute, Orchestrator–workers, Supervisor | LangGraph | UC4, UC11 | [ ] |
| W22 | Evaluator–optimizer, Guardrail sandwich, Dual LLM, HITL | — | UC3, UC7, UC12 | [ ] |

## Books
- *Head First Design Patterns* 2e ⭐ · refactoring.guru ⭐ · *Design Patterns* (GoF, reference)
- *Patterns of Enterprise Application Architecture* (Fowler) · *Learning Domain-Driven Design* (Khononov)
- ⭐ *Patterns of Distributed Systems* (Unmesh Joshi): WAL, leases, high-water mark, quorum, generation clock
- *Microservices Patterns* (Richardson) · *Enterprise Integration Patterns* (Hohpe) · *Cloud Design Patterns* (Microsoft Azure Architecture Center, free)
- *Concurrency in Go* · *Java Concurrency in Practice* · Anthropic *Building effective agents*
