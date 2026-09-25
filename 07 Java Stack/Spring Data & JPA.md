---
tags: [java, spring, jpa, database]
phase: 2
---
# 🗃️ Spring Data & JPA / Hibernate

## Core → Advanced
- [ ] Entity mapping, relationships (`@OneToMany`, `@ManyToOne`, owning side), `mappedBy`
- [ ] Entity lifecycle: transient → managed → detached → removed; persistence context (1st-level cache); dirty checking
- [ ] Fetching: LAZY vs EAGER, **N+1 problem**, `JOIN FETCH`, `@EntityGraph`, batch fetching
- [ ] Transactions: `@Transactional` propagation (REQUIRED, REQUIRES_NEW), isolation, read-only, rollback rules
- [ ] Locking: optimistic (`@Version`), pessimistic (`PESSIMISTIC_WRITE` → `SELECT … FOR UPDATE`, `SKIP LOCKED`)
- [ ] Projections (interface/DTO/record), pagination (Slice vs Page, keyset)
- [ ] Specifications / Querydsl for dynamic queries
- [ ] Batch inserts (`hibernate.jdbc.batch_size`, sequence ID generation)
- [ ] Second-level cache (awareness), open-session-in-view (**disable it**)
- [ ] Migrations with **Flyway** (or Liquibase); expand/contract for zero-downtime deploys
- [ ] When to skip JPA: **jOOQ** or `JdbcClient` for complex SQL
- [ ] HikariCP pool sizing

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 SQL logging on; create an N+1 on workflow → steps; fix it 3 ways
- [ ] 🟡 Optimistic locking on workflow publish: 50 concurrent publishes → exactly one wins
- [ ] 🔴 Keyset pagination over 5M runs; compare with offset at page 10,000
- [ ] 🔴 An outbox table written in the same transaction as the domain change
- [ ] ⚫ Rewrite the heaviest query with jOOQ or `JdbcClient`; compare the SQL and speed

## 🧠 Cognitive tasks
- [ ] Predict the SQL Hibernate will emit for 5 repository methods before running them
- [ ] Symptom → hypotheses: "a save() in a loop is slow and memory grows"

## 🛰️ Orbit integration
- [ ] Workflow versions, runs, and prompts repositories in orbit-api

> [!info] Go deeper
> ⚙️ [[Spring Internals]] · [[PostgreSQL Internals]] · 🧩 [[Enterprise & DDD Patterns]]

## Resources
- Vlad Mihalcea: *High-Performance Java Persistence* + blog ⭐
- Thorben Janssen's blog · Spring Data JPA reference
