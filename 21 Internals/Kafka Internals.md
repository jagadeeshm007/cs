---
tags: [internals, kafka]
week: W11
---
# 📨 Kafka Internals (important parts only)

## 1. Storage: the log
- Topic → partitions → each partition is a directory of **segments**: `.log` (records in batches), `.index` (sparse offset → file position), `.timeindex`
- **Append-only, sequential writes**; reads mostly hit the **OS page cache**; **zero-copy** (`sendfile`) to consumers when not using TLS
- Retention by time/size deletes whole old segments; **log compaction** keeps the latest value per key (a cleaner thread; tombstones = null values)
- Why Kafka is fast: sequential I/O + page cache + **batching** + **compression per batch** + zero-copy + partition parallelism

## 2. Replication
- Each partition has a **leader** and followers; followers **pull** (fetch) from the leader
- **ISR** (in-sync replicas): followers caught up within `replica.lag.time.max.ms`
- **LEO** (log end offset) per replica; **high watermark (HW)** = the highest offset replicated to all ISR → **consumers only see up to the HW**
- `acks=all` + `min.insync.replicas=2` (RF=3) → a write succeeds only when ≥ 2 replicas have it
- **Leader epochs** make followers truncate divergent logs after a leader change
- `unclean.leader.election.enable=false` → prefer unavailability over data loss

## 3. Control plane: KRaft
- Metadata (topics, partitions, ISR, configs) lives in the `__cluster_metadata` log, replicated by **Raft** across controller nodes; brokers replicate that log. ZooKeeper is gone as of Kafka 4.0

## 4. Producer
- `send()` → serializer → **partitioner** (murmur2(key) % partitions; sticky batching for null keys) → **RecordAccumulator** (a batch per partition) → **sender thread** ships batches when `batch.size` is reached or `linger.ms` expires
- **Idempotent producer** (default on): producer ID + a per-partition **sequence number** → the broker drops duplicates from retries; ordering is preserved with ≤ 5 in-flight requests
- **Transactions**: `transactional.id` → a transaction coordinator (`__transaction_state`); writes to many partitions + consumer offsets commit atomically; **control records** (commit/abort markers); `read_committed` consumers read up to the **LSO** (last stable offset)

## 5. Consumer
- A pull-based `poll()` loop; `fetch.min.bytes`/`fetch.max.wait.ms`; `max.poll.records`
- Liveness: a heartbeat thread (`session.timeout.ms`) **and** poll progress (`max.poll.interval.ms`); slow processing → kicked from the group → rebalance
- **Group coordinator**; offsets stored in `__consumer_offsets` (compacted)
- Rebalancing: eager (stop-the-world) → **cooperative incremental** → the **new consumer group protocol** (KIP-848, server-side assignment)
- Delivery: commit **after** processing = at-least-once → make handlers **idempotent**

## 🔬 Prove it
- [ ] 3-broker KRaft cluster in Docker; `kafka-topics --describe` → kill the leader → watch the ISR shrink and a new leader get elected
- [ ] **Data loss experiment**: `acks=1`, kill the leader right after writes → count lost messages; repeat with `acks=all`, `min.insync.replicas=2` → zero loss
- [ ] Inspect segments with `kafka-dump-log.sh --files … --print-data-log`; find batches, compression, and producer IDs
- [ ] Throughput vs `linger.ms` (0, 5, 20) and compression (none/lz4/zstd): plot it
- [ ] Slow consumer exceeding `max.poll.interval.ms` → observe the rebalance → fix it with smaller batches or pause/resume
- [ ] Ordering test: key = runId across 6 partitions, scale consumers 1 → 3 → 6
- [ ] Transactions: read-process-write with `read_committed`; abort midway and show consumers never see the aborted records

## Interview questions #interview-q
How Kafka guarantees ordering · the HW vs LEO · `acks` + `min.insync.replicas` trade-offs · how idempotent producers work · exactly-once in Kafka (and its limits outside Kafka) · why Kafka is fast · rebalancing problems · Kafka vs RabbitMQ
