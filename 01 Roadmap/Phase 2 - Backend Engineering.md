---
tags: [roadmap, phase]
weeks: W5–W9
dates: 2026-10-26 → 2026-11-29
---
# Phase 2: Backend Engineering (W5–W9)

> [!goal] Exit criteria
> - Build a production-grade Spring Boot service: layered/hexagonal structure, validation, error handling, security, migrations, integration tests
> - Build the same kind of service in Go without a heavy framework
> - Design a PostgreSQL schema, choose indexes, read `EXPLAIN ANALYZE`, and prevent lost updates under concurrency (optimistic locking, RLS, idempotency keys)
> - Explain JWT vs sessions, the OAuth2 authorization code + PKCE flow, and OIDC
> - Pick REST vs gRPC vs GraphQL for a use case and defend the choice
> - Build a tool-calling loop from scratch and stream LLM tokens end to end
> - **Ship [[Orbit v1 - Core Platform]]**


## 🔥 This phase's work
| Track | Where |
|---|---|
| 🎯 Weekly assignments, labs, cognitive tasks, open questions | [[Assignments - Phase 2]] (A5–A9) |
| ⚙️ Internals | [[Spring Internals]] · [[PostgreSQL Internals]] · [[Redis Internals]] |
| 🧩 Design patterns | [[Enterprise & DDD Patterns]] · [[GoF Patterns (Java & Go)]] (Proxy, Chain, Composite, Interpreter) |
| ⚫ Boss fight | 200 concurrent streaming chats + 50 runs/s: find and fix 2 bottlenecks with JFR + pprof |
| 🧠 Daily/weekly drills | [[Cognitive Drills]] · self-grade with [[Grading Rubric]] |

## Tracks
- Java: [[Spring Core & Boot]] · [[Spring Data & JPA]] · [[Spring Security]]
- Go: [[Go Backend Development]]
- APIs: [[REST API Design]] · [[gRPC & Protobuf]] · [[GraphQL]] · [[Realtime (WebSockets, SSE)]]
- Data: [[PostgreSQL]] · [[Redis]]
- Infra: [[Docker]] (compose level)
- Side: [[Frontend Essentials]] (8 hrs total)
- DSA: trees, heaps, backtracking, graphs I/II

## Reading
- *Spring Start Here* (Spilcă) if Spring internals feel shaky, then *Spring in Action* 6e (Walls) selectively
- *Spring Security in Action* 2e (Spilcă)
- *Let's Go* + *Let's Go Further* (Alex Edwards): the best practical Go web books
- *Use The Index, Luke* (free) + PostgreSQL docs ch. 11 (Indexes), ch. 13 (Concurrency Control)
- *The Missing README* (Riccomini & Ryaboy): how real teams work

## Key engineering habits to adopt now
- [ ] Conventional commits, small PRs to yourself, protected main branch
- [ ] Every feature ships with tests (unit + Testcontainers integration)
- [ ] Every non-obvious decision gets an ADR ([[Design Docs & ADRs]])
- [ ] Structured JSON logging with correlation IDs from day one

## Retro
- What stuck:
- What didn't:
- Skill Matrix delta:
