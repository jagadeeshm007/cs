---
tags: [assignments, cognitive, mindset]
---
# 🧠 Cognitive Drills: train the engineer's thought process

> [!important] Why
> Knowledge is cheap (AI can recite it). **What gets you hired and promoted is how you think**: predicting behavior, reasoning under uncertainty, finding root causes, and making trade-offs explicit. These drills train that deliberately.

## The 14 drills
| # | Drill | How | Example |
|---|---|---|---|
| 1 | **Predict → Verify** ⭐ | Before any experiment, write a prediction with numbers. Run it. Explain the gap | "Halving the Hikari pool from 20 → 10 will raise p99 from 40 ms to ~?" |
| 2 | **Feynman teach-back** | Explain a concept in 3 min, out loud, no notes; record it; note where you stumbled | "Explain MVCC to a junior" |
| 3 | **Blank-page design** | Design a system from memory on paper in 20 min, *then* compare with references | "Design Kafka" |
| 4 | **Constraint flip** | Take a finished design and change one constraint: 100× traffic, strong consistency, ½ budget, multi-region, 10 ms latency | "Orbit engine with 1M runs/s?" |
| 5 | **Pre-mortem** | "It's 6 months later and this failed badly. Why?" List 10 causes, rank them, mitigate the top 3 | Before each Orbit version ships |
| 6 | **Symptom → hypotheses** | Given symptoms only, write 3–5 ranked hypotheses + the cheapest test for each | "p99 spikes every 30 s, CPU flat" |
| 7 | **Reverse engineering** | Read a product's behavior/API and infer its architecture *before* reading its engineering blog | Discord message storage, Stripe idempotency |
| 8 | **Trade-off debate** | Write the best argument **for** and **against** an option, then decide | "Kafka vs Postgres queue for tasks" |
| 9 | **Fermi estimation** | 5-minute order-of-magnitude estimates with explicit assumptions | "Tokens/day for 10k tenants × 50 runs" |
| 10 | **Code archaeology** | Read unfamiliar source, draw the call graph, and explain one design decision | `ThreadPoolExecutor.execute()` |
| 11 | **Compression** | Summarize a chapter/paper in 5 bullets, then in 1 sentence | DDIA ch. 7 |
| 12 | **Transfer** | Apply an idea from domain A to domain B | "Kafka's HW idea → Orbit's safe-to-archive marker" |
| 13 | **First-principles derivation** | Derive why a mechanism must exist from the failure it prevents | "Why does Raft need terms?" |
| 14 | **Self-review after 7 days** | Reread your ADR/code from last week as a critical reviewer; write 3 critiques | Every Sunday |

## Routine
- **Daily (15 min):** 1 Predict→Verify during Build time + 1 Fermi or teach-back
- **Weekly (60 min, Saturday):** Blank-page design + Constraint flip on that week's topic
- **Per Orbit version:** Pre-mortem before, self-review after

## Drill log
| Date | Drill | Topic | Prediction / claim | Reality / critique | Lesson |
|---|---|---|---|---|---|
| | | | | | |

## Prompt bank: symptom → hypotheses (drill 6)
- p99 latency spikes every ~30 s; CPU and QPS flat
- Kafka consumer lag grows only for 1 of 12 partitions
- After a deploy, 1% of requests 502 for ~20 s
- Postgres CPU 90%, the same query count as yesterday
- Memory of a Go service grows 50 MB/hour, never drops
- A Java service with virtual threads has lower throughput than with platform threads
- The LLM gateway shows TTFT doubling at 3 pm daily
- RAG answers got worse after re-ingesting the same documents
- An agent occasionally performs the same tool action twice
- gRPC traffic all goes to one of 5 pods
