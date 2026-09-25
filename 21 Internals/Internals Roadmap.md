---
tags: [internals, moc]
---
# ⚙️ Internals Roadmap: only what matters

> [!important] Why internals
> Interviewers at top companies ask "how does it work?" to tell users apart from engineers. More importantly, **you can't debug what you can't model**. This track covers only the internals that explain real production behavior (latency spikes, data loss, outages) and that come up in interviews.

## The internals study method (per mechanism)
1. **Question**: write down what you want to explain (e.g. "why does Kafka lose data with `acks=1`?")
2. **Model**: read the design doc/source and draw the mechanism (boxes, arrows, state)
3. **Predict**: write what you expect an experiment to show
4. **Prove**: run the experiment in the note's "🔬 Prove it" list
5. **Explain**: 3-minute teach-back out loud, plus a 5-line summary in `Notes/`

## Schedule
| Week | Internals note | Focus |
|---|---|---|
| W1–W2 | [[JVM Internals]] | Memory, GC, JIT, JMM, HashMap/CHM, AQS, virtual threads |
| W1 | [[Linux & OS Internals]] | Syscalls, virtual memory, page cache, epoll, cgroups |
| W3 | [[Go Runtime Internals]] | Scheduler, stacks, channels, GC, maps, interfaces |
| W3–W4 | [[Network Stack Internals]] | TCP, TLS 1.3, HTTP/2, gRPC framing |
| W4–W6 | [[PostgreSQL Internals]] | MVCC, WAL, vacuum, indexes, locks, planner |
| W5–W7 | [[Spring Internals]] | Context refresh, bean lifecycle, proxies, MVC, Security, JPA |
| W8 | [[Redis Internals]] | Event loop, encodings, expiry, persistence, cluster |
| W11 | [[Kafka Internals]] | Log segments, replication/ISR/HW, idempotence, transactions, rebalancing |
| W15 | [[Container Internals]] | Namespaces, cgroups, overlayfs, OCI, runc |
| W15 | [[Kubernetes Internals]] | API server, etcd, informers, scheduler, kubelet, Services |
| W16 | [[Envoy Internals]] | Threading, filter chains, xDS, pools, circuit breaking |
| W19 | [[LLM Inference Internals]] | Prefill/decode, KV cache, batching, sampling, embeddings/HNSW |

## Source code worth reading (1 file per week, ~1 hour each)
`java.util.HashMap` · `ConcurrentHashMap` · `AbstractQueuedSynchronizer` · `ThreadPoolExecutor` · Spring `AbstractApplicationContext.refresh()` · `AbstractAutowireCapableBeanFactory.doCreateBean()` · `DispatcherServlet.doDispatch()` · Go `runtime/chan.go` · `runtime/proc.go` (skim `schedule()`/`findRunnable()`) · `sync/mutex.go` · `net/http/server.go` · `context/context.go` · franz-go producer · Kafka `Partition.scala`/`ReplicaManager` (skim) · client-go `tools/cache` (informers) · etcd `raft` package (skim)
