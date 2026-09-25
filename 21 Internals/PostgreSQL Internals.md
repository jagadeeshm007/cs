---
tags: [internals, postgres, database]
week: W4–W6
---
# 🐘 PostgreSQL Internals (important parts only)

## 1. Process model
- The postmaster **forks one backend process per connection** (MBs each + a context switch) → connections are expensive → **pool** (HikariCP/pgxpool + PgBouncer)
- Shared memory: **shared_buffers** (page cache); background processes: checkpointer, background writer, WAL writer, autovacuum launcher/workers, WAL senders (replication)

## 2. Storage
- Tables/indexes = files of **8 KB pages**; a page has line pointers → **tuples**
- Tuple header: **`xmin`** (inserting txn), **`xmax`** (deleting/locking txn), `ctid` (physical location)
- Large values → **TOAST** (compressed/out-of-line)

## 3. MVCC
- UPDATE = **insert a new tuple version + mark the old one's `xmax`** (no in-place update)
- **Snapshot**: which txn IDs were committed when it was taken; visibility = f(xmin, xmax, snapshot, commit log)
- Read Committed: new snapshot **per statement** · Repeatable Read: one snapshot **per transaction** (+ serialization errors on conflicting updates) · Serializable: **SSI** tracks read-write dependencies and aborts dangerous structures
- **Readers never block writers, and writers never block readers**
- **HOT updates**: if no indexed column changed and the page has room, the new version stays on the same page → no index update (tune `fillfactor`)

## 4. VACUUM
- Dead tuples stay until **VACUUM** marks the space reusable (it doesn't shrink files; `VACUUM FULL`/pg_repack rewrite them)
- Updates the **visibility map** (enables **index-only scans**) and the free space map
- **Freezing** prevents 32-bit **transaction ID wraparound** (an emergency shutdown if ignored)
- Long-running transactions or stale replication slots **block cleanup** → bloat

## 5. WAL (write-ahead log)
- Changes are written to the WAL **before** data pages; commit = WAL flushed (`synchronous_commit`); data pages are written later by the checkpointer
- Crash recovery = replay WAL from the last checkpoint; **full-page writes** after each checkpoint protect against torn pages
- Streaming replication = shipping WAL; **logical decoding** (used by **Debezium CDC**) reads WAL via **replication slots** → ⚠️ an abandoned slot retains WAL forever → the disk fills up

## 6. Indexes & planner
- **B-tree** (Lehman-Yao, concurrent-friendly); GIN (jsonb, arrays, full-text), GiST, BRIN (huge append-only tables), **HNSW/IVFFlat via pgvector**
- The **planner** estimates row counts from **statistics** (`ANALYZE`: histograms, most-common values, n_distinct) → costs plans → picks seq/index/bitmap scans and nested loop/hash/merge joins
- Bad estimates (correlated columns, stale stats) → bad plans → `CREATE STATISTICS`, `ANALYZE`

## 7. Locks
- Row locks live in the tuple (`xmax` + multixact), not in memory → unlimited row locks
- Table-level lock modes; **the lock queue**: an `ALTER TABLE` waiting for `ACCESS EXCLUSIVE` blocks **every** later query → use `lock_timeout` in migrations ⭐
- Deadlock detector runs after `deadlock_timeout`; advisory locks for app-level coordination

## 🔬 Prove it
- [ ] `SELECT ctid, xmin, xmax, * FROM t;` → update a row → see the new ctid/xmin; `pageinspect` → see the dead tuple
- [ ] Reproduce non-repeatable read (RC), a lost update, and **write skew** (RR) → fix with SERIALIZABLE or `FOR UPDATE`
- [ ] Hold a transaction open for 10 min while updating a hot table → watch bloat (`pg_stat_user_tables.n_dead_tup`) → commit → VACUUM
- [ ] Lock-queue outage: a long SELECT + `ALTER TABLE ADD COLUMN` + new SELECTs → all block → fix with `lock_timeout`
- [ ] Create a logical replication slot, stop consuming, and watch `pg_replication_slots` retain WAL
- [ ] Stale-statistics bad plan → `ANALYZE` → a plan change in `EXPLAIN`
- [ ] Index-only scan appears only after VACUUM updates the visibility map

## Interview questions #interview-q
How MVCC works in Postgres · why VACUUM exists · isolation levels + anomalies (write skew!) · what WAL is and how replication/CDC use it · why connections are expensive · why a migration took down production (the lock queue)
