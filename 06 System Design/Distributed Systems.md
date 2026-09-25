---
tags: [system-design, distributed-systems]
phase: 3
---
# 🌍 Distributed Systems

## Core → Advanced
- [ ] **The 8 fallacies of distributed computing**
- [ ] Failure models: crash, omission, Byzantine; partial failures; timeouts as the only failure detector
- [ ] Replication: single-leader, multi-leader, leaderless (Dynamo-style); sync vs async; replication lag anomalies (read-your-writes, monotonic reads)
- [ ] Partitioning: range vs hash, consistent hashing, rebalancing, hot spots, secondary indexes (local vs global)
- [ ] Consistency models: linearizable → sequential → causal → eventual; read-your-writes
- [ ] CAP (properly understood) and PACELC
- [ ] Quorums: W + R > N; sloppy quorums, hinted handoff, read repair, anti-entropy (Merkle trees)
- [ ] Time: physical clocks, NTP skew, Lamport clocks, vector clocks, hybrid logical clocks, TrueTime
- [ ] Consensus: Raft (leader election, log replication, safety), Paxos awareness; etcd/ZooKeeper
- [ ] Distributed transactions: 2PC (and why it blocks), sagas, outbox
- [ ] Delivery semantics: at-most/at-least/exactly-once; **idempotency** and dedupe keys
- [ ] Distributed locks and fencing tokens (Kleppmann's critique of Redlock)
- [ ] CRDTs and collaborative editing (awareness)
- [ ] Multi-region: active-passive, active-active, conflict resolution, cell-based architecture

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟡 MIT 6.5840 Lab 1 MapReduce (W10) · Lab 2 KV server (W12)
- [ ] 🔴 Gossip Glomers: broadcast (3a–3e), grow-only counter, Kafka-style log
- [ ] ⚫ MIT 6.5840 **Lab 3 Raft** (3A–3D) · Lab 4 (open assignment)
- [ ] 🔴 Network partition with `tc netem` / iptables between replicated Postgres nodes
- [ ] ⚫ Porcupine linearizability checking on your KV

## 🧠 Cognitive tasks
- [ ] First-principles: derive why Raft needs terms, log matching, and majority commits
- [ ] Reverse engineering: infer DynamoDB's design from its API guarantees, then read the paper
- [ ] Constraint flip: make Orbit's engine strongly consistent across 2 regions. What does it cost?

## 🛰️ Orbit integration
- [ ] Leases + fencing tokens, idempotency keys, outbox, and sagas in [[Orbit v2 - Durable Workflows]]

> [!info] Go deeper
> ⚙️ [[Kafka Internals]] · [[Kubernetes Internals]] · 🧩 [[Distributed & Cloud Patterns]]

## Resources
- ⭐ *DDIA* ch. 5–9 · *Understanding Distributed Systems* (Vitillo)
- Martin Kleppmann's Cambridge *Distributed Systems* lectures (YouTube, free)
- MIT 6.5840 schedule + papers (pdos.csail.mit.edu/6.824)
- Papers: Raft, Dynamo, Spanner, Chubby → [[Engineering Blogs & Papers]]
- Jepsen analyses (jepsen.io): see how real databases break
