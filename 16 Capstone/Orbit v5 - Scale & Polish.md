---
tags: [capstone, orbit]
version: v5
weeks: W23–W24
---
# Orbit v5: Scale & Polish (Phase 6)

- [ ] Load: 1,000 concurrent runs + 500 concurrent streams (mock LLM provider with realistic latency distributions)
- [ ] Profile (JFR, async-profiler, pprof, `EXPLAIN`, ClickHouse query log) → fix the top 3 bottlenecks → re-test → write a "scaling journal"
- [ ] Partition the event-history table (by time/hash); archive completed runs to S3 (claim check)
- [ ] "100× plan" doc: cell-based architecture (tenant → cell routing), sharded engine, multi-region control plane, cost model
- [ ] Cost model: $/run by use case at 1M runs/month
- [ ] Portfolio README: problem, architecture, 12 hard problems + how you solved them, numbers, demo, how to run it
- [ ] Pin the repo; link it from your resume and LinkedIn; publish the blog series

## Interview stories this project gives you → [[Behavioral & STAR]]
Exactly-once effects · lease/fencing bug found in chaos testing · noisy-neighbor fairness · streaming through proxies · RAG quality from 0.6 to 0.9 recall · a prompt-injection fix · cost cut by 40% · Java vs Go trade-off
