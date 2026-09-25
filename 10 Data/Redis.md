---
tags: [data, redis, cache]
phase: 2
---
# 🟥 Redis

## Core → Advanced
- [ ] Data structures: strings, hashes, lists, sets, sorted sets (leaderboards, rate limits), bitmaps, HyperLogLog, geo, streams
- [ ] Single-threaded event loop (+ I/O threads); why it's fast; big-key and hot-key problems
- [ ] TTLs and eviction policies (LRU/LFU variants)
- [ ] Caching patterns: cache-aside, read-through, write-through, write-behind; invalidation strategies
- [ ] **Cache stampede** prevention: locking/singleflight, probabilistic early expiry, jittered TTLs
- [ ] Transactions (`MULTI/EXEC`), **Lua scripts** / Functions for atomic ops
- [ ] Distributed locks: `SET NX PX` + fencing tokens; Redlock controversy
- [ ] Rate limiting: fixed window, sliding log, sliding window counter, token bucket (Lua)
- [ ] Pub/Sub vs **Streams** (consumer groups)
- [ ] Persistence: RDB vs AOF; replication; Sentinel vs **Cluster** (hash slots)
- [ ] Pipelining; client-side caching
- [ ] Vector search in Redis (awareness); semantic caching for LLMs
- [ ] Licensing landscape: Redis vs **Valkey** fork (know that Valkey exists and is used by AWS/Google)

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 `OBJECT ENCODING`/`MEMORY USAGE` experiments
- [ ] 🟡 Token-bucket quotas in Lua with hash tags per tenant (cluster-safe)
- [ ] 🔴 A semantic cache index (vector search) vs an exact cache for the gateway
- [ ] ⚫ Build your own Redis (Go): replication or RDB stage

## 🧠 Cognitive tasks
- [ ] Predict the pipelining speedup; explain it with RTT math

## 🛰️ Orbit integration
- [ ] Gateway quotas + cache, orbit-stream pub/sub + resume buffers, API-key revocation

> [!info] Go deeper
> ⚙️ [[Redis Internals]]

## Resources
- redis.io docs + Redis University (free) · *Redis in Action* (dated but conceptually good)
