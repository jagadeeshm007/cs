---
tags: [data, postgres]
phase: 2
---
# 🐘 PostgreSQL (your default database)

## Core → Advanced
- [ ] SQL fluency: joins, CTEs, window functions, `GROUP BY`/`HAVING`, `LATERAL`, upserts (`ON CONFLICT`)
- [ ] Schema design: normalization (to 3NF) and deliberate denormalization; constraints (FK, UNIQUE, CHECK, exclusion constraints ⭐ for seat/time overlaps)
- [ ] Data types: `jsonb`, arrays, `uuid`, `timestamptz` (always), `numeric` for money, enums
- [ ] Indexes: B-tree, composite ordering, partial, covering (`INCLUDE`), expression, GIN (jsonb/full-text), GiST, BRIN
- [ ] `EXPLAIN (ANALYZE, BUFFERS)`: seq scan vs index scan vs bitmap; row estimates; join strategies
- [ ] MVCC, VACUUM/autovacuum, bloat, transaction ID wraparound (awareness)
- [ ] Isolation levels in Postgres (Read Committed default; Repeatable Read = snapshot; Serializable = SSI)
- [ ] Locks: row locks, `FOR UPDATE`, `SKIP LOCKED` (job queues), advisory locks, deadlock detection
- [ ] Connection pooling: HikariCP / pgxpool + **PgBouncer** (transaction mode caveats)
- [ ] Replication: streaming (physical), logical replication; read replicas; failover (Patroni awareness)
- [ ] Partitioning (declarative, range/list/hash); when to shard (Citus awareness)
- [ ] Full-text search (`tsvector`); **pgvector** for embeddings ⭐
- [ ] Observability: `pg_stat_statements`, `pg_stat_activity`, slow query log, `auto_explain`
- [ ] Backups: `pg_dump` vs PITR (WAL archiving)
- [ ] Zero-downtime migrations (add a column nullable → backfill → constraint; `CREATE INDEX CONCURRENTLY`)

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 pgexercises.com (all sections)
- [ ] 🟡 5M-row `runs`/`run_events`: optimize 5 queries with EXPLAIN; before/after
- [ ] 🔴 An RLS multi-tenancy + cross-tenant test suite
- [ ] 🔴 A `SKIP LOCKED` task queue with leases; partition `run_events` by month
- [ ] ⚫ Zero-downtime migration drill: add a NOT NULL column + an index to a hot table under load (`lock_timeout`, `CONCURRENTLY`)

## 🧠 Cognitive tasks
- [ ] Predict → verify plans, lock waits, and bloat
- [ ] Symptom → hypotheses: "DB CPU 90%, same QPS as yesterday"

## 🛰️ Orbit integration
- [ ] Control plane DB, engine event history, pgvector for RAG

> [!info] Go deeper
> ⚙️ [[PostgreSQL Internals]] · [[Database Internals]]

## Resources
- PostgreSQL docs ⭐ (very high quality) · *Use The Index, Luke* ⭐ · *The Art of PostgreSQL* (Fontaine)
- *PostgreSQL 14 Internals* (Rogov, free) · Crunchy Data + pganalyze blogs · CMU 15-445
