---
tags: [cs, databases]
phase: 1
---
# 🗄️ Database Internals

## Core → Advanced
- [ ] Storage: pages, heap files, B+ trees vs LSM trees (write vs read amplification)
- [ ] WAL (write-ahead log), checkpoints, crash recovery
- [ ] Indexes: clustered vs secondary, composite (leftmost prefix), covering, partial, hash, GIN/GiST
- [ ] ACID in depth
- [ ] Isolation levels and anomalies: dirty read, non-repeatable read, phantom, lost update, **write skew**
- [ ] MVCC (Postgres tuples/xmin/xmax, vacuum) vs locking
- [ ] Query planning: cost-based optimizer, statistics, join algorithms (nested loop, hash, merge)
- [ ] Replication: sync/async, logical vs physical, replication lag
- [ ] Partitioning vs sharding; consistent hashing
- [ ] Connection pooling (HikariCP, PgBouncer) and why connections are expensive in Postgres

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 Reproduce every isolation anomaly with two `psql` sessions
- [ ] 🟡 `pageinspect`: watch xmin/xmax/ctid change across UPDATE/DELETE
- [ ] 🔴 *Build Your Own Database From Scratch in Go* (build-your-own.org): B+tree + KV
- [ ] ⚫ Tiny LSM in Go: memtable + WAL + SSTables + compaction; compare with bbolt

## 🧠 Cognitive tasks
- [ ] Trade-off debate: B-tree vs LSM for Orbit's append-heavy event history
- [ ] Predict → verify: index-only scan before and after VACUUM

## 🛰️ Orbit integration
- [ ] The `run_events` table design (append-only, partitioning plan)
- [ ] Isolation level choice for lease acquisition

> [!info] Go deeper
> ⚙️ [[PostgreSQL Internals]] · [[Redis Internals]]

## Resources
- *Database Internals* (Alex Petrov)
- *DDIA* ch. 3 (Storage) and ch. 7 (Transactions) ⭐
- CMU 15-445 (Andy Pavlo) lectures on YouTube ⭐
- *PostgreSQL 14 Internals* (Egor Rogov, free PDF)
Related: [[PostgreSQL]]
