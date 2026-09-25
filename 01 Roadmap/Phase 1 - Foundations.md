---
tags: [roadmap, phase]
weeks: W1–W4
dates: 2026-09-28 → 2026-10-25
---
# Phase 1: Foundations (W1–W4)

> [!goal] Exit criteria (you pass the phase when you can...)
> - Explain how `HashMap`, `ConcurrentHashMap`, and GC work, and when to use virtual threads vs platform threads
> - Write idiomatic, concurrent Go (worker pools, context cancellation, no goroutine leaks)
> - Solve easy/medium array, string, stack, binary-search, and linked-list problems in < 20 min
> - Explain what happens when you type a URL in a browser, down to TCP/TLS/HTTP
> - Explain B-tree vs LSM, MVCC, and the four isolation levels with their anomalies
> - Finish an LLD machine-coding round (Parking Lot) in 90 min with clean OOP + tests
> - **Ship [[Orbit v0 - Building Blocks]]** and beat the **1BRC boss fight** in Java and Go


## 🔥 This phase's work
| Track | Where |
|---|---|
| 🎯 Weekly assignments, labs, cognitive tasks, open questions | [[Assignments - Phase 1]] (A1–A4) |
| ⚙️ Internals | [[JVM Internals]] · [[Go Runtime Internals]] · [[Linux & OS Internals]] · [[Network Stack Internals]] |
| 🧩 Design patterns | [[GoF Patterns (Java & Go)]] · [[Concurrency Patterns]] |
| ⚫ Boss fight | 1 Billion Row Challenge in Java + Go (< 10 s each) |
| 🧠 Daily/weekly drills | [[Cognitive Drills]] · self-grade with [[Grading Rubric]] |

## Why this phase matters
Everything later (Spring, Kafka, K8s, AI) is an abstraction over these foundations. Senior engineers debug by reasoning from first principles, and that reasoning needs this layer.

## Tracks
- Languages: [[Java Advanced]] · [[Go Advanced]] · [[Python Essentials]]
- CS: [[Operating Systems]] · [[Networking]] · [[Concurrency]] · [[Database Internals]]
- DSA: [[DSA Roadmap (Java)]] (W1–W4 section)
- Design: [[Low-Level Design & Machine Coding]]
- Mindset: [[Engineering Thinking Framework]] · [[How to Learn (Read-Build-Write-Teach)]]

## Reading for this phase
- *Effective Java* (Bloch): items on objects, generics, lambdas, concurrency
- *Java Concurrency in Practice* (Goetz) ch. 1–5, 16 (still the best source on the JMM)
- *Learning Go* 2e (Bodner) + *Concurrency in Go* (Cox-Buday)
- *Operating Systems: Three Easy Pieces* (free): virtualization + concurrency sections
- *Head First Design Patterns* 2e

## Hands-on deliverables
- [ ] `kv-store-java`: in-memory KV with TTL, LRU eviction, thread-safe, benchmarked with JMH
- [ ] `crawler-go`: concurrent crawler with worker pool, rate limit, context cancellation
- [ ] `lld-solutions`: repo with Parking Lot, Splitwise, Elevator, Snake & Ladder (Java, tests)
- [ ] Build your own Redis (Go), first stages: TCP server, RESP protocol, GET/SET/EXPIRE

## Retro
- What stuck:
- What didn't:
- Skill Matrix delta:
