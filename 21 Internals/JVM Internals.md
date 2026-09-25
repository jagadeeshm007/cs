---
tags: [internals, java, jvm]
week: W1–W2
---
# ☕ JVM Internals (important parts only)

## 1. Class loading
- **Load → Link (verify, prepare, resolve) → Initialize** (`<clinit>` runs once, thread-safe, which is why the holder-class singleton idiom works)
- Class loaders: bootstrap → platform → application; **parent delegation**. Spring Boot fat jars use a custom loader to read nested jars
- `ClassNotFoundException` vs `NoClassDefFoundError` (found at compile time, missing or failed init at runtime)

## 2. Execution: interpreter + tiered JIT
- Bytecode starts **interpreted** → hot methods go to **C1** (fast compile, profiling) → very hot methods go to **C2** (aggressive optimizations using the profile)
- Key optimizations: **inlining** (the mother of all optimizations), **escape analysis** (scalar replacement: no heap allocation if the object doesn't escape), loop unrolling, lock elision, intrinsics
- **Deoptimization**: when a speculative assumption breaks (a new subclass loads), code goes back to the interpreter. This is why benchmarks need warmup → use **JMH**
- Startup work: CDS/AppCDS, Project Leyden AOT caches, GraalVM native image (closed-world, no JIT warmup)

## 3. Memory layout
| Area | What | Tuning/problems |
|---|---|---|
| Heap | Objects; young (eden + survivors) + old | `-Xmx`, `MaxRAMPercentage` in containers |
| Metaspace | Class metadata (native memory) | Leaks via classloaders (hot redeploy) |
| Thread stacks | Frames per platform thread (~1 MB reserved) | 10k platform threads = lots of memory → virtual threads |
| Code cache | JIT-compiled code | Full code cache → JIT stops → slow |
| Direct memory | NIO buffers (Netty) | `MaxDirectMemorySize`; invisible in heap dumps |
- **Object header**: mark word (hash, lock bits, GC age) + class pointer; compressed oops; *compact object headers* (JDK 25) shrink headers
- **TLAB**: each thread bump-pointer allocates in its own buffer, which makes allocation almost free. GC cost is about **live** objects, not dead ones

## 4. Garbage collection
- **Generational hypothesis**: most objects die young → cheap copying of survivors in young GC
- **G1** (default): heap split into regions; remembered sets + card tables track old→young pointers; concurrent marking (SATB); **mixed collections** reclaim the old regions with the most garbage first; pause-time goal (`MaxGCPauseMillis`)
- **ZGC** (generational): colored pointers + **load barriers** → concurrent relocation → sub-millisecond pauses regardless of heap size; costs some throughput and CPU
- **Safepoints**: stop-the-world points; time-to-safepoint can dominate pauses (long counted loops)
- What to read in GC logs (`-Xlog:gc*`): pause times, allocation rate, promotion rate, heap after GC (growing = leak)

## 5. Java Memory Model (JMM)
- Without synchronization, the compiler/CPU may **reorder** and threads may see **stale values**
- **Happens-before** rules: program order · monitor unlock → subsequent lock · volatile write → subsequent read · `Thread.start()` → actions in the thread · actions → `join()` return · final field freeze in constructors
- **Safe publication**: via `volatile`, `final`, locks, concurrent collections, static init
- Double-checked locking is broken without `volatile` (a partially constructed object is visible)

## 6. Locks & synchronizers
- `synchronized` → object monitor: thin lock via CAS on the mark word → inflates to a heavyweight OS-backed monitor under contention (biased locking was removed)
- **AQS (`AbstractQueuedSynchronizer`)**: one `volatile int state` + a CLH-style FIFO wait queue of parked threads; `ReentrantLock`, `Semaphore`, `CountDownLatch`, `ReentrantReadWriteLock` are all built on it ⭐ read the source
- CAS + `LongAdder` (striped counters beat `AtomicLong` under contention)

## 7. Virtual threads (Loom)
- A virtual thread is a **continuation** scheduled on carrier threads (a ForkJoinPool, ~#cores)
- On blocking I/O or `LockSupport.park`, the stack frames are copied to the heap and the carrier is freed → millions of cheap threads
- **Pinning**: native frames still pin the carrier (synchronized no longer pins since JDK 24, JEP 491). Detect it with the JFR event `jdk.VirtualThreadPinned`
- Rules: don't pool virtual threads; limit concurrency with semaphores (not pool size); be careful with heavy `ThreadLocal`s; no benefit for CPU-bound work

## 8. Collections internals
- **HashMap**: `table[]` of nodes; `hash = h ^ (h >>> 16)`; index `(n-1) & hash`; a bucket becomes a **red-black tree at 8 entries** (if capacity ≥ 64); resize doubles and splits buckets into lo/hi lists without rehashing; not thread-safe (lost updates, and infinite loops in old JDKs)
- **ConcurrentHashMap**: CAS into empty bins, `synchronized` on the bin head for collisions, cooperative multi-thread resize with forwarding nodes, `CounterCell`s for size
- **ArrayList** grows 1.5×; `ArrayDeque` circular buffer; `PriorityQueue` binary heap in an array
- **String**: compact strings (Latin-1 `byte[]`), immutable, the intern pool

## 🔬 Prove it
- [ ] **JOL** (Java Object Layout): print the layout of `Integer`, `String`, a `HashMap.Node`; compute the memory of 1M `HashMap<Integer,Integer>` entries, then verify with a heap histogram (`jcmd <pid> GC.class_histogram`)
- [ ] JMH: a method allocating a non-escaping object vs an escaping one; watch allocation rate with `-prof gc`
- [ ] `-XX:+PrintCompilation` + a hot loop: watch tiers change; trigger deoptimization by loading a new subclass
- [ ] Run the same service with G1 vs generational ZGC under load; compare p99 and CPU
- [ ] Write a racy `boolean running` flag without `volatile` in a JIT-hot loop → it never stops → fix it
- [ ] 100k virtual threads doing `Thread.sleep` vs 100k platform threads; then a pinned virtual thread (native call) → JFR event
- [ ] Heap-dump a deliberate leak (static map) and find it in Eclipse MAT (dominator tree)

## Interview questions #interview-q
HashMap internals and Java 8 changes · CHM vs `synchronizedMap` · what `volatile` guarantees (and doesn't) · G1 vs ZGC · how virtual threads work, and pinning · what escape analysis does · diagnose high GC CPU · the class loading order and static init
