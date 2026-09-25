---
tags: [patterns, concurrency, java, go]
---
# 🔀 Concurrency Patterns (Java + Go)

| Pattern | Problem | Java | Go | Orbit usage |
|---|---|---|---|---|
| **Producer–consumer** | Decouple production from consumption | `BlockingQueue` | Buffered channel | Engine → task queue → workers |
| **Worker pool** | Bounded parallelism | `ThreadPoolExecutor` / virtual threads + `Semaphore` | N goroutines reading one channel | Step runners |
| **Pipeline** | Stage-by-stage streaming | `CompletableFuture` chains, Reactor | Chained channels | Ingestion: parse → chunk → embed → upsert |
| **Fan-out / fan-in** | Parallelize and merge | `invokeAll`, structured concurrency | Multiple goroutines + merge channel | `map` step, parallel sub-agents |
| **Bounded concurrency (semaphore)** | Cap concurrent calls | `Semaphore` | Buffered channel as a semaphore, `x/sync/semaphore` | Max concurrent LLM calls per tenant |
| **Futures / promises** | Async results | `CompletableFuture` | Channel of results, `errgroup` | Parallel tool calls |
| **Structured concurrency** | Child tasks scoped to a parent; cancel siblings on failure | `StructuredTaskScope` (check its status in your JDK) | `errgroup.WithContext` ⭐ | Parallel steps: fail fast |
| **Cancellation / deadlines** | Stop wasted work | `Future.cancel`, interrupts | ⭐ `context.Context` | Run cancellation propagates to LLM streams |
| **Request coalescing (singleflight)** | Dedupe identical concurrent work | Caffeine `AsyncLoadingCache` | `x/sync/singleflight` ⭐ | Cache stampede protection in the gateway |
| **Backpressure** | Don't let producers overwhelm consumers | Bounded queues + rejection policy, Reactive Streams | Blocking sends on bounded channels | Streaming tokens to slow clients; 429 admission |
| **Rate limiting** | Smooth the request rate | Guava `RateLimiter`, bucket4j | `x/time/rate` | Provider RPM/TPM limits |
| **Actor** | State owned by one thread, message passing | Akka/Pekko | A goroutine owning state + an inbox channel | Per-run coordinator |
| **Reactor (event loop)** | Many connections, few threads | Netty | Go netpoller (hidden) | orbit-stream |
| **Read–write lock** | Many readers, few writers | `ReentrantReadWriteLock`, `StampedLock` | `sync.RWMutex` | Provider config registry |
| **Copy-on-write** | Lock-free reads of rarely-changing data | `CopyOnWriteArrayList` | `atomic.Pointer[T]` swap | Routing table hot reload |
| **Lock striping** | Reduce contention | CHM bins, `LongAdder` | Sharded maps with N mutexes | In-memory quota counters |
| **Optimistic concurrency (CAS / version)** | Avoid locks under low contention | `AtomicReference`, JPA `@Version` | `atomic.CompareAndSwap`, SQL version columns | Workflow publish, lease renewals |
| **Double-checked locking** | Lazy init | Needs `volatile`; prefer the holder idiom | `sync.Once` | Lazy provider clients |
| **Thread confinement** | No sharing, no locks | `ThreadLocal`, scoped values | Goroutine-local by design | Request context |
| **Immutable objects** | Safe sharing | Records | Value types, unexported fields | Workflow definitions after publish |
| **Guarded suspension / condition wait** | Wait until a condition holds | `Condition.await` | `sync.Cond` / channels | Waiting for a lease/slot |
| **Heartbeat** | Liveness | Scheduled executor | `time.Ticker` goroutine | Worker lease renewal |

## 🔬 Katas
- [ ] Pipeline with a bounded channel per stage; prove backpressure (a slow last stage → producers block, memory stays flat)
- [ ] `errgroup` fan-out with cancel-on-first-error vs Java structured concurrency: the same behavior, compared
- [ ] singleflight: 1,000 concurrent identical cache misses → 1 upstream call
- [ ] Copy-on-write config reload under 10k RPS without locks
- [ ] Actor-style run coordinator in Go vs lock-based in Java: compare complexity and bugs
