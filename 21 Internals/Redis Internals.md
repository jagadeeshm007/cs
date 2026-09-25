---
tags: [internals, redis]
week: W8
---
# 🟥 Redis Internals (important parts only)

## 1. Execution model
- **Single-threaded command execution** on an event loop (epoll) → every command is **atomic** → no locks
- I/O threads (6.0+) can parallelize socket reads/writes, but execution stays single-threaded
- Consequence: **one slow command blocks everyone** → avoid `KEYS *` (use `SCAN`), huge `HGETALL`/`SMEMBERS`, deleting big keys synchronously (`UNLINK` = lazy free)
- Lua scripts / Functions run atomically too, so keep them short

## 2. Data structure encodings (memory vs speed)
| Type | Small encoding | Large encoding |
|---|---|---|
| String | int / embstr / raw (**SDS**: length-prefixed, binary-safe) | |
| Hash | **listpack** (compact contiguous) | hashtable |
| List | listpack | **quicklist** (linked list of listpacks) |
| Set | **intset** / listpack | hashtable |
| Sorted set | listpack | **skiplist + hashtable** (O(log n) ranks + O(1) score lookup) |
- Conversions happen at thresholds (`hash-max-listpack-entries`, etc.): small objects are very memory-efficient
- The hashtable uses **incremental rehashing** (two tables, migrated a bit per operation) → no big pause

## 3. Expiry & eviction
- Expiry: **lazy** (checked on access) + an **active expire cycle** (samples keys with TTLs, repeats if many were expired)
- Eviction (`maxmemory-policy`): **approximated** LRU/LFU by sampling `maxmemory-samples` keys; LFU uses a probabilistic counter with decay

## 4. Persistence
- **RDB**: `fork()` + **copy-on-write** snapshot → a memory spike proportional to the write rate during the snapshot; fork latency on large heaps
- **AOF**: append every write; `appendfsync everysec` (≤ 1 s of loss) vs `always` (slow); background AOF rewrite compacts it
- Durability ≠ the main use case: treat Redis as a cache/ephemeral coordinator unless you've designed for it

## 5. Replication & cluster
- **Async** replication with a replication backlog + `PSYNC` partial resync; `WAIT` for synchronous-ish acks (still not strong consistency)
- **Cluster**: **16,384 hash slots** (CRC16(key) mod 16384); **hash tags** `{tenant42}:quota` keep related keys in one slot (required for multi-key ops/Lua); `MOVED`/`ASK` redirects; gossip bus; replica promotion on failure
- Failover can **lose acknowledged writes** (async) → distributed locks on Redis need fencing tokens

## 🔬 Prove it
- [ ] `OBJECT ENCODING` on a hash as it grows past the listpack threshold; `MEMORY USAGE` before/after
- [ ] `redis-benchmark` with and without pipelining (`-P 16`) → explain the throughput jump (RTTs)
- [ ] Put 1M elements in a list, `DEL` it while another client does GETs → measure the latency spike → repeat with `UNLINK`
- [ ] `SLOWLOG GET`, `LATENCY DOCTOR` after a `KEYS *` on 1M keys
- [ ] Trigger `BGSAVE` under heavy writes, watch RSS and `INFO persistence` (`latest_fork_usec`)
- [ ] Your Lua token bucket: 200 concurrent goroutines → prove there's no over-admission

## Interview questions #interview-q
Why Redis is fast despite being single-threaded · how expiry works · RDB vs AOF · cluster hash slots and hash tags · why Redlock is controversial · the cache stampede and how to prevent it
