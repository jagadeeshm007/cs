---
tags: [mindset, core]
---
# 🧠 Engineering Thinking Framework

> [!quote] The core shift
> Juniors ask *"how do I build this?"* Seniors ask *"what problem are we solving, what does it cost, and what happens when it breaks?"*

## The loop (use it for every feature, design, and interview)
1. **Understand the problem.** Who is the user? What is the job to be done? What does success look like, and how is it measured?
2. **Clarify constraints.** Scale (QPS, data size, growth), latency, consistency, availability, cost, team size, deadline, compliance.
3. **Find the core difficulty.** Every system has 1–3 hard parts (e.g. exactly-once effects, hot keys, fan-out). Spend 80% of your thinking there.
4. **Generate ≥ 2 options.** Never go with the first idea. Include the "boring" option.
5. **Compare trade-offs explicitly.** Use a table: complexity, cost, latency, consistency, operability, reversibility. See [[Trade-offs Cheat Sheet]].
6. **Decide and record it.** Write an ADR ([[Design Docs & ADRs]]). Name what you are giving up.
7. **Build the smallest thing that proves it.** Spike, prototype, benchmark.
8. **Measure.** Metrics, traces, load tests. Opinions don't count, data does ([[Optimization Principles]]).
9. **Iterate.** Evolve the design as real constraints show up.

## First-principles questions
- What must be true for this to work? What's the physical limit (network RTT, disk IOPS, memory bandwidth)?
- What is the **source of truth**? Everything else is a cache or a projection.
- What happens on **failure**: timeout, retry, duplicate, partial write, out-of-order delivery?
- What's the **blast radius** if this component dies?
- What is **reversible** and what isn't? (A one-way door deserves slow thinking; a two-way door deserves speed.)
- What is the simplest thing that could possibly work? What would make it no longer work?

## Product thinking (end to end, start to scale)
| Stage | Users | Architecture | Focus |
|---|---|---|---|
| 0 → 1 | 0–1k | Modular monolith, one Postgres, managed hosting | Speed of learning, correctness, simplicity |
| 1 → 10 | 1k–100k | Add cache, read replicas, background jobs, CDN, observability | Performance, reliability, on-call basics |
| 10 → 100 | 100k–10M | Split services along team/domain boundaries, event streaming, sharding | Team autonomy, scalability, SLOs |
| 100+ | 10M+ | Multi-region, cells, platform teams, custom infra | Efficiency, resilience, cost |

> [!warning] The classic mistake
> Designing for stage 100 while you're at stage 0. Microservices, Kafka, and K8s have real costs. In Orbit you'll build every stage deliberately so you **feel** why each step happens.

## Mental models worth internalizing
- **Conway's Law**: systems mirror the communication structure of the organizations that build them
- **Gall's Law**: a complex system that works evolved from a simple system that worked
- **Hyrum's Law**: every observable behavior of your API will be depended on by someone
- **Amdahl's Law**: speedup is bounded by the part you didn't parallelize
- **Little's Law**: L = λ × W (concurrency = throughput × latency). This is how you size pools and queues.
- **Second-order effects**: retries → retry storms; caches → thundering herd; autoscaling → cold starts
- **Chesterton's Fence**: understand why something exists before you remove it

## Habits of top engineers
- Read code more than you write it (read Spring, Kafka client, or Go stdlib source on purpose)
- Write things down: design docs, post-mortems, notes
- Own outcomes, not tickets
- Ask "how would I know if this is broken in production?" before you merge
- Keep a brag document (feeds [[Behavioral & STAR]])
