---
tags: [cs, concurrency, java, go]
phase: 1
---
# 🔀 Concurrency (language-agnostic + Java + Go)

## Concepts
- [ ] Concurrency vs parallelism
- [ ] Race conditions, critical sections, atomicity, visibility, ordering
- [ ] Memory models: happens-before (Java JMM, Go memory model)
- [ ] Locks: mutex, RW-lock, reentrant, spin locks; lock contention; lock-free with CAS
- [ ] Deadlock, livelock, starvation; lock ordering
- [ ] Models: shared memory + locks · message passing (CSP, Go channels) · actors · async/await
- [ ] Producer–consumer, bounded buffers, backpressure
- [ ] Thread pools, work stealing (ForkJoinPool), Little's Law for pool sizing

## Java specifics
- [ ] `synchronized`, `volatile`, `java.util.concurrent` (locks, atomics, latches, semaphores, `ConcurrentHashMap`)
- [ ] `ExecutorService`, `CompletableFuture` composition, cancellation
- [ ] **Virtual threads** (Java 21+): when they help (I/O bound) and when they don't (CPU bound), pinning
- [ ] **Structured concurrency** and **scoped values** (check the status in your JDK version: preview vs final)

## Go specifics
- [ ] Goroutines + the scheduler (G-M-P model), channels (buffered/unbuffered), `select`
- [ ] `sync.Mutex`, `RWMutex`, `WaitGroup`, `Once`, `sync/atomic`, `errgroup`
- [ ] `context` for cancellation/deadlines; preventing goroutine leaks
- [ ] Patterns: pipeline, fan-out/fan-in, worker pool, semaphore via buffered channel, rate limiting
- [ ] Race detector: `go test -race`

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 Even/odd printer with 2 threads; dining philosophers (Java + Go)
- [ ] 🟡 Bank transfer deadlock → fix it with lock ordering → `tryLock` with timeout
- [ ] 🟡 Bounded blocking queue: Java (`ReentrantLock` + `Condition`) and Go (channels)
- [ ] 🔴 A concurrent LRU in both languages + benchmarks + `jcstress` / `-race`
- [ ] ⚫ Pipeline with backpressure: prove memory stays flat when the last stage is slow

## 🧠 Cognitive tasks
- [ ] Predict → verify: throughput of 1 mutex vs 16 stripes vs `LongAdder` at 32 threads
- [ ] First-principles: derive why `volatile` alone can't make `count++` safe
- [ ] Reverse engineering: how does `singleflight` avoid a thundering herd? Draw it

## 🛰️ Orbit integration
- [ ] Worker pool + semaphore limits per tenant in orbit-worker
- [ ] Cancellation propagation from run cancel → LLM stream close

> [!info] Go deeper
> ⚙️ [[JVM Internals]] · [[Go Runtime Internals]] · 🧩 [[Concurrency Patterns]]

## Resources
- *Java Concurrency in Practice* (Goetz) ⭐
- *Concurrency in Go* (Cox-Buday) ⭐
- Jenkov's Java concurrency tutorials; Go blog "Share Memory By Communicating"
- *The Art of Multiprocessor Programming*: advanced, optional
