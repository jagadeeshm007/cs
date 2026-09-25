---
tags: [patterns, ddd, enterprise, architecture]
---
# 🏢 Enterprise, Application & DDD Patterns

## Application structure
| Pattern | What | When | Orbit usage |
|---|---|---|---|
| **Layered** | Controller → service → repository | Simple CRUD | Admin CRUD |
| **Hexagonal (Ports & Adapters)** ⭐ | Domain core; ports = interfaces; adapters = web/DB/LLM/Kafka | Core domains with many integrations | Engine core independent of Postgres/Kafka |
| **Clean / Onion** | Dependency rule points inward | Same idea, more ceremony | — |
| **Vertical slices** | Organize by feature | Many independent features | Use-case modules |
| **Modular monolith** ⭐ | Enforced module boundaries in one deployable | Default start | orbit-api with Spring Modulith |

## Data access (Fowler, PoEAA)
| Pattern | Notes |
|---|---|
| **Repository** | A collection-like interface for aggregates (Spring Data) |
| **Unit of Work** | Track changes, commit once (Hibernate Session / persistence context) |
| **Identity Map** | One object per row per session (first-level cache) |
| **Data Mapper vs Active Record** | JPA/sqlc (mapper) vs Rails-style (record) |
| **Lazy Load** | Proxies; the root of N+1 |
| **Specification** | Composable query predicates (Spring Data Specifications) |
| **DTO / projection** | Shape data for the API; never leak entities |
| **Transaction Script vs Domain Model** | Procedural per use case vs rich objects; choose by domain complexity |

## DDD, strategic
- [ ] **Bounded context** (Orbit: Tenancy, Workflow Authoring, Execution, Knowledge, Tooling, Billing)
- [ ] **Ubiquitous language** (run, step, attempt, lease, signal)
- [ ] **Context map**: customer/supplier, conformist, **anti-corruption layer** (around LLM provider APIs!), shared kernel, published language (protobuf events)
- [ ] Subdomains: core (execution engine) vs supporting (tool registry) vs generic (auth → buy Keycloak)

## DDD, tactical
| Pattern | Rule | Orbit example |
|---|---|---|
| **Entity** | Identity over time | `Run`, `Workflow` |
| **Value object** | Immutable, equality by value | `TokenUsage`, `Money`, `RetryPolicy` |
| **Aggregate** ⭐ | A consistency boundary; modify one aggregate per transaction; reference others by ID | `Run` (with its steps) |
| **Domain event** | Something happened (past tense) | `StepCompleted`, `ApprovalRequested` |
| **Domain service** | Logic that doesn't fit an entity | `RoutingPolicyEvaluator` |
| **Factory** | Complex creation with invariants | `Run.start(definitionVersion, input)` |

## Integration patterns
**Outbox** · **Inbox / idempotent receiver** · **Saga** (orchestration/choreography) · **Process manager** · **CQRS** · **Event sourcing** · **Materialized view** · **API composition** · **BFF** · **Strangler fig** · **Branch by abstraction** · **Feature toggles** → details in [[Distributed & Cloud Patterns]]

## 🔬 Katas
- [ ] Draw Orbit's context map with the relationship types
- [ ] Find an aggregate boundary mistake: put `Workflow` and `Run` in one aggregate → contention analysis → split them
- [ ] ArchUnit tests that enforce hexagonal rules in orbit-api (domain must not import Spring/JPA)
- [ ] Write the same use case as a Transaction Script and as a Domain Model; list the trade-offs
