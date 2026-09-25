---
tags: [language, java]
phase: 1
---
# ☕ Java Advanced (target: JDK 25 LTS)

## 1. Language mastery
- [ ] OOP deeply: encapsulation, composition over inheritance, immutability
- [ ] Generics: bounded types, wildcards, PECS, type erasure
- [ ] Modern Java: `var`, records, sealed classes, pattern matching for `switch`/`instanceof`, record patterns, text blocks
- [ ] Streams & collectors (and when **not** to use them), Optional done right
- [ ] Functional interfaces, lambdas, method references
- [ ] Exceptions: checked vs unchecked, try-with-resources, exception design
- [ ] `equals`/`hashCode` contracts, `Comparable` vs `Comparator`
- [ ] Annotations & reflection (needed to understand Spring)
- [ ] Modules (JPMS): awareness level

## 2. Collections internals
- [ ] `HashMap`: hashing, buckets, treeification, resize, load factor
- [ ] `ConcurrentHashMap`: CAS + bin-level locking
- [ ] `ArrayList` vs `LinkedList` vs `ArrayDeque`; `TreeMap` (red-black); `PriorityQueue` (binary heap)
- [ ] `LinkedHashMap` access order → LRU in 10 lines

## 3. JVM
- [ ] Class loading, bytecode, JIT (C1/C2), tiered compilation
- [ ] Memory: heap (young/old), metaspace, stacks, direct memory
- [ ] GC: G1 (default), ZGC (generational, low pause), Parallel. How to choose; reading GC logs
- [ ] JFR + JDK Mission Control, async-profiler, heap dumps (Eclipse MAT)
- [ ] Container awareness: `MaxRAMPercentage`, CPU limits
- [ ] GraalVM native image / CDS / Project Leyden for startup time (awareness)

## 4. Concurrency → [[Concurrency]]
- [ ] JMM, happens-before, `volatile`, `synchronized`, `java.util.concurrent`
- [ ] Virtual threads (Project Loom), structured concurrency, scoped values
- [ ] `CompletableFuture` pipelines

## 5. Tooling & quality
- [ ] Maven **and** Gradle (Kotlin DSL); multi-module builds
- [ ] JUnit 5, AssertJ, Mockito, Testcontainers, ArchUnit, JMH
- [ ] Static analysis: SpotBugs / Error Prone / SonarLint

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 JOL: print object layouts; compute the memory of 1M `HashMap` entries
- [ ] 🟡 Implement `HashMap` (with resize + treeify-lite) and `ArrayList` from scratch with tests
- [ ] 🟡 JMH: streams vs loops, boxing costs, escape analysis (`-prof gc`)
- [ ] 🔴 Platform vs virtual threads under a blocking load; then detect pinning with JFR
- [ ] 🔴 Read `ConcurrentHashMap.putVal` + `AbstractQueuedSynchronizer`; write a 1-page explanation
- [ ] ⚫ **1BRC in Java** (W4 boss fight)

## 🧠 Cognitive tasks
- [ ] Predict → verify: GC pause p99 with G1 vs generational ZGC on the same load
- [ ] Code archaeology: `ThreadPoolExecutor.execute()`; draw its 3 branches
- [ ] Transfer: where does the JDK use the Decorator, Strategy, and Template Method patterns?

## 🛰️ Orbit integration
- [ ] `orbit-kv` + `MiniThreadPool` (W1–W2)
- [ ] orbit-api on virtual threads with sensible concurrency limits

> [!info] Go deeper
> ⚙️ [[JVM Internals]] · [[Spring Internals]] · 🧩 [[GoF Patterns (Java & Go)]] · [[Concurrency Patterns]]

## Resources
- *Effective Java* 3e (Bloch) ⭐ · *Java Concurrency in Practice* ⭐ · *Modern Java in Action*
- dev.java, Inside Java (podcast/blog), JEP index, José Paumard's JEP Café (YouTube)
- Baeldung (reference), *Optimizing Java* (Evans et al.)

## Interview questions #interview-q
- How does `HashMap` work? What changed in Java 8?
- `volatile` vs `synchronized` vs `AtomicInteger`?
- When would virtual threads **not** help?
- How would you diagnose a memory leak in production?
