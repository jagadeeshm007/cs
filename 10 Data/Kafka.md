---
tags: [data, kafka, streaming]
phase: 3
---
# 📨 Apache Kafka

## Core → Advanced
- [ ] Log-based messaging: topics, partitions, offsets, segments, retention, compaction
- [ ] Brokers, replication factor, ISR, `acks`, `min.insync.replicas`; leader election; **KRaft** (no ZooKeeper)
- [ ] Producers: partitioner, keys → ordering per key, batching (`linger.ms`, `batch.size`), compression, **idempotent producer**
- [ ] Consumers: consumer groups, rebalancing (cooperative sticky), offset commits (auto vs manual), lag
- [ ] Delivery semantics: at-least-once + idempotent consumers (default), **transactions / exactly-once** (read-process-write)
- [ ] Error handling: retry topics, **DLQ**, poison pills
- [ ] Schema management: **Schema Registry** + Avro/Protobuf; compatibility modes
- [ ] Kafka Connect + **Debezium CDC** → [[Data Pipelines]]
- [ ] Kafka Streams (Java) / stream processing concepts: windows, joins, state stores
- [ ] Sizing: partitions count, throughput, consumer parallelism ≤ partitions
- [ ] Ops: monitoring lag, under-replicated partitions, rebalance storms
- [ ] Alternatives: Redpanda, Pulsar, NATS JetStream, SQS/SNS, RabbitMQ (know when each fits)
- [ ] Newer features: share groups / queues for Kafka (KIP-932), tiered storage (awareness)

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 A 3-broker KRaft cluster; kill the leader; watch the ISR
- [ ] 🟡 The data-loss experiment with `acks=1` vs `acks=all` + `min.insync.replicas`
- [ ] 🔴 Outbox → Debezium → Protobuf events with Schema Registry; evolve a schema safely
- [ ] 🔴 Retry topics + a DLQ + a replay CLI for webhooks
- [ ] ⚫ Gossip Glomers Kafka-style log; CodeCrafters "Build your own Kafka"

## 🧠 Cognitive tasks
- [ ] Predict ordering during rebalances; verify
- [ ] Trade-off debate: Kafka vs a Postgres queue for tasks

## 🛰️ Orbit integration
- [ ] `run.events`, `usage.events`, triggers, run-search projection, analytics feed

> [!info] Go deeper
> ⚙️ [[Kafka Internals]] · 🧩 [[Distributed & Cloud Patterns]]

## Resources
- *Kafka: The Definitive Guide* 2e ⭐ · **Confluent Developer** free courses ⭐
- Jay Kreps, "The Log: What every software engineer should know about real-time data's unifying abstraction" ⭐
- Kafka paper (LinkedIn, 2011)
