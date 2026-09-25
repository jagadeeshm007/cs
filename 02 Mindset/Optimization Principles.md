---
tags: [mindset, performance]
---
# ⚡ Optimization Principles

> [!important] Rule 0
> **Measure → find the bottleneck → fix the biggest one → measure again.** Premature optimization wastes effort, but so does ignoring performance until it's too late. Set performance budgets early.

## 1. Know the numbers (orders of magnitude)
| Operation | ~Latency |
|---|---|
| L1 cache ref | 1 ns |
| Main memory ref | 100 ns |
| Compress 1 KB (fast codec) | 2 µs |
| Read 1 MB sequentially from memory | ~10 µs |
| SSD random read | 16–100 µs |
| Round trip within the same datacenter | 0.5 ms |
| Read 1 MB sequentially from SSD | ~50 µs–1 ms |
| Redis GET over network | ~0.2–1 ms |
| Indexed Postgres query | 1–5 ms |
| Cross-region round trip (e.g. Mumbai ↔ US-East) | 150–250 ms |
More in [[Estimation Cheatsheet]].

## 2. The optimization ladder (cheapest, highest-impact first)
1. **Don't do the work.** Remove features, avoid calls, lazy-load
2. **Do less work.** Better algorithm/data structure (O(n²) → O(n log n)), pagination, projections (select only needed columns)
3. **Do it once.** Caching (CPU cache → in-process → Redis → CDN), memoization, precomputation/materialized views
4. **Do it in bulk.** Batching (DB inserts, Kafka producer `linger.ms`), pipelining (Redis), connection pooling
5. **Do it later.** Async/queues, background jobs, write-behind
6. **Do it in parallel.** Concurrency, partitioning, sharding. Watch Amdahl and contention.
7. **Do it closer.** Data locality, CDN/edge, read replicas in the user's region
8. **Do it on better hardware.** Vertical scaling. Often the cheapest fix for real.

## 3. Common backend bottlenecks & fixes
| Symptom | Likely cause | Fix |
|---|---|---|
| Slow list endpoints | N+1 queries | Join fetch / batch loading / DataLoader |
| High DB CPU | Missing/wrong index, seq scans | `EXPLAIN ANALYZE`, composite/partial/covering indexes |
| p99 latency spikes | GC pauses, lock contention, pool exhaustion | GC tuning (ZGC), reduce allocation, size pools with Little's Law |
| Timeouts under load | Unbounded queues, no backpressure | Bounded queues, load shedding, rate limits |
| Cache stampede | Hot key expires | Request coalescing (singleflight), jittered TTL, early refresh |
| Hot partition | Bad shard key | Better key, key salting, split hot tenants |
| Memory growth | Leaks, unbounded caches, goroutine leaks | Profilers (JFR, pprof), bounded caches (Caffeine), context cancellation |

## 4. Methods for analysis
- **USE** (for resources): Utilization, Saturation, Errors (Brendan Gregg)
- **RED** (for services): Rate, Errors, Duration
- **Four golden signals**: latency, traffic, errors, saturation
- Always look at **percentiles (p50/p95/p99)**, never only averages
- Tools: JFR + JDK Mission Control, async-profiler, JMH (Java); `pprof`, `trace`, `benchstat` (Go); `EXPLAIN (ANALYZE, BUFFERS)`; k6/Gatling; flame graphs

## 5. Code-level principles
- Choose the right data structure first; it matters more than micro-optimizations
- Reduce allocations in hot paths (Go: preallocate slices, `sync.Pool`; Java: avoid boxing and needless streams in tight loops)
- Avoid chatty I/O; prefer fewer, larger calls
- Set timeouts on **every** network call, and use bounded retries with exponential backoff + jitter
- Keep hot data compact and contiguous (cache-friendly)

## 6. Cost is a performance metric too (FinOps)
Every design has a monthly bill. Estimate it: compute + storage + egress + managed services. Senior engineers optimize for **cost per request**.

Related: [[SRE & Reliability]] · [[Observability]] · [[PostgreSQL]] · [[Redis]]
