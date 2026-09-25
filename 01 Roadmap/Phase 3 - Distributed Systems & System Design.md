---
tags: [roadmap, phase]
weeks: W10–W14
dates: 2026-11-30 → 2027-01-03
---
# Phase 3: Distributed Systems & System Design (W10–W14)

> [!goal] Exit criteria
> - Run a 45-min system design interview with the framework in [[System Design Roadmap]]: requirements → estimates → API → data model → HLD → deep dives → bottlenecks
> - Explain replication (leader/follower, multi-leader, leaderless), partitioning, consistency models, CAP/PACELC, and quorum math
> - Implement Raft leader election (MIT 6.5840 Lab 3A) in Go
> - Use Kafka correctly: partition keys, ordering, consumer groups, rebalancing, at-least-once + idempotency, DLQs
> - Implement outbox + saga and explain why 2PC is avoided
> - Have 12+ case studies in `Notes/` using the *System Design Case* template
> - Build a durable engine with leases + fencing tokens that survives `kill -9` chaos
> - **Ship [[Orbit v2 - Durable Workflows]]**


## 🔥 This phase's work
| Track | Where |
|---|---|
| 🎯 Weekly assignments, labs, cognitive tasks, open questions | [[Assignments - Phase 3]] (A10–A14) |
| ⚙️ Internals | [[Kafka Internals]] · [[PostgreSQL Internals]] |
| 🧩 Design patterns | [[Distributed & Cloud Patterns]] |
| ⚫ Boss fight | Chaos Day: 5,000 runs with random kills/failovers → 0 lost runs, 0 duplicate effects |
| 🧠 Daily/weekly drills | [[Cognitive Drills]] · self-grade with [[Grading Rubric]] |

## Tracks
- Theory: [[Distributed Systems]] · [[Building Blocks]] · [[Estimation Cheatsheet]]
- Patterns: [[Architecture Patterns]] · [[Spring Cloud & Microservices]] · [[Go Microservices & Tooling]]
- Data: [[Kafka]] · [[Search & Other Stores]]
- Practice: [[Case Studies]]
- DSA: DP I–III, greedy, intervals, tries, bits

## Reading (the core of your architecture education)
- ⭐ *Designing Data-Intensive Applications* (Kleppmann; 2nd ed. with Riccomini if available). Read ch. 1–9 slowly and write a note per chapter
- *Understanding Distributed Systems* (Vitillo): short, very clear, read it first as a warm-up
- *System Design Interview* Vol 1 & 2 (Alex Xu): case-study practice
- *Microservices Patterns* (Chris Richardson): saga, outbox, CQRS
- *Building Microservices* 2e (Newman): ch. on splitting, communication, resiliency
- Papers: Raft, Dynamo, Kafka (see [[Engineering Blogs & Papers]])
- Lectures: Martin Kleppmann's *Distributed Systems* (Cambridge) on YouTube; MIT 6.5840 lectures

## Retro
- What stuck:
- What didn't:
- Skill Matrix delta:
