---
tags: [assignments, phase-1]
weeks: W1–W4
---
# 📝 Assignments: Phase 1 (Foundations)

> Each week: **🎯 Assignment** (graded with the [[Grading Rubric]]) · **🔬 Lab** · **🧠 Cognitive task** · **🌀 Open question** (no single right answer; write a 1-page answer in `Notes/`)

## W1 - Concurrent KV Store (Java)
**🎯 A1** Build `orbit-kv`: an in-memory key-value store.
- [ ] `GET/SET/DEL/EXPIRE/TTL` over a RESP-like TCP protocol, one **virtual thread** per connection
- [ ] TTL: lazy expiry on read + an active expiry sampler thread (Redis-style)
- [ ] Max-entries **LRU eviction** (your own doubly linked list + map, not `LinkedHashMap`)
- [ ] Thread safety via **lock striping** (N segments)
- [ ] Tests: 64 threads × 100k random ops, with a model-based checker for invariants
- [ ] JMH: ops/s for 1/8/64 threads; striped vs single global lock
- **Acceptance:** no lost updates; ≥ 1M ops/s in-process on your machine (8 threads); clean shutdown
- **Stretch:** `jcstress` test for your LRU's `get`

**🔬 Lab:** JOL + `jcmd GC.class_histogram`: the real memory per entry in your store vs `HashMap<String,String>` ([[JVM Internals]])
**🧠 Cognitive:** *Predict → Verify*: predict the throughput ratio between the global lock and 16 stripes at 64 threads, then measure and explain the gap
**🌀 Open:** LRU fails on scan-heavy workloads. Research LFU, **W-TinyLFU** (Caffeine) and ARC. Which would you choose for an LLM response cache, and why?
**Score:** __/28

## W2 - Thread Pool & Rate Limiters (Java)
**🎯 A2** Build a `MiniThreadPool` and `orbit-ratelimit`.
- [ ] Pool: core/max workers, a bounded queue, 3 rejection policies, graceful `shutdown()`/`shutdownNow()`, worker death recovery
- [ ] `BoundedBlockingQueue` using `ReentrantLock` + two `Condition`s
- [ ] Rate limiters: token bucket, sliding-window log, sliding-window counter; one shared test-vector file (JSON) that the Go version will reuse
- [ ] Benchmark: 10k blocking tasks (sleep 50 ms) on platform pool(200) vs virtual threads vs your pool
- **Acceptance:** no deadlocks under a 10-minute stress run; rate limiters within ±2% of the target rate
- **Stretch:** read `ThreadPoolExecutor.execute()` and write down its 3 branches

**🔬 Lab:** a racy counter → fix it with `synchronized`, `AtomicLong`, and `LongAdder`; JMH under 1/4/32 threads
**🧠 Cognitive:** *Feynman*: explain the 6 happens-before rules and double-checked locking in 3 minutes. Record it
**🌀 Open:** Design a **distributed** rate limiter for 50 gateway replicas: exact (Redis on every request) vs approximate (local buckets + periodic sync). What's the error bound, and when is each acceptable?
**Score:** __/28

## W3 - DAG Executor & Expression Language (Go)
**🎯 A3** Build `orbit-dag`, the seed of Orbit's engine.
- [ ] Input: workflow JSON (steps + `depends_on`); **topo sort with cycle detection** (Kahn)
- [ ] Execute ready steps concurrently with a **bounded worker pool** (semaphore)
- [ ] Per-step timeout (`context.WithTimeout`), retries with **exponential backoff + full jitter**, cancel all on a fatal failure (`errgroup`)
- [ ] Step outputs are available to downstream steps (`steps.<id>.output`)
- [ ] `orbit-expr`: lexer + Pratt parser + evaluator for `&&, ||, ==, >, !, .field, [index]`, used in `when:` conditions
- [ ] `go test -race` clean; **`goleak`** verifies no leaked goroutines after cancellation
- **Acceptance:** a 1,000-step random DAG executes in the correct order; a failure cancels in-flight steps within 50 ms
- **Stretch:** port the rate limiter to Go and pass the shared JSON test vectors

**🔬 Lab:** `GODEBUG=schedtrace=1000` + `-gcflags=-m` on your executor ([[Go Runtime Internals]])
**🧠 Cognitive:** *Predict*: which variables in your executor escape to the heap? List them first, then verify
**🌀 Open:** Your executor loses all progress if the process crashes. Write 1 page: what's the minimal set of things to persist to resume safely? (You'll build this in W10.)
**Score:** __/28

## W4 - Mini Redis, LLD Rounds & the 1BRC Boss Fight
**🎯 A4**
- [ ] **Mini Redis in Go**: PING, ECHO, SET/GET with PX, concurrent clients, RESP parsing with `bufio`; pass the CodeCrafters/codingchallenges stages
- [ ] **2 timed LLD rounds (90 min each, Java)**: Parking Lot, Splitwise. Then an Orbit LLD: classes for `Workflow`, `Step`, `Run`, `StepExecutor` (Strategy), `RetryPolicy`, `StepState` (State)
- [ ] Reproduce **all isolation anomalies** in Postgres (dirty read is impossible in PG, so explain why), lost update, non-repeatable read, phantom, **write skew**

**⚫ Phase boss fight: 1 Billion Row Challenge** in Java **and** Go
- Baseline → profile → optimize (custom parsing, memory-mapped files, parallel chunks, custom hash map)
- **Acceptance:** Java < 10 s and Go < 10 s on your machine (the top results are far faster); write-up with each optimization and its measured gain

**🧠 Cognitive:** *Blank-page*: write "what happens when you type a URL" in 15 min at full depth, then compare with [[Network Stack Internals]]
**🌀 Open:** B-tree vs LSM for Orbit's **append-heavy run event history**: argue both sides, then decide
**Score:** __/28
