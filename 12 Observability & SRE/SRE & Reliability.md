---
tags: [ops, sre, reliability, performance]
phase: 4
---
# 🛡️ SRE, Reliability & Performance

## Reliability
- [ ] SLI → SLO → SLA; **error budgets** and error budget policies
- [ ] Toil, on-call, incident response (roles: IC, comms, ops), **blameless post-mortems**
- [ ] Failure modes: cascading failures, retry storms, thundering herds, metastable failures
- [ ] Resilience patterns → [[Architecture Patterns]]
- [ ] Capacity planning (Little's Law, load tests, headroom)
- [ ] Graceful degradation & load shedding (e.g. disable recommendations when the DB is overloaded)
- [ ] **Chaos engineering**: hypotheses, blast radius; tools: Chaos Mesh, Litmus, toxiproxy
- [ ] DR: RPO/RTO, backups tested by restores
- [ ] Deploy safety: canaries, feature flags, automatic rollback

## Performance engineering
- [ ] Load testing with **k6** (or Gatling for Java): load, stress, spike, soak tests
- [ ] Profiling: JFR/async-profiler, Go pprof, flame graphs
- [ ] Find and fix: DB (indexes, pools), caching, serialization, GC, lock contention
- [ ] Write up a performance report: goal → setup → results → bottleneck → fix → new results

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟡 SLOs: run success, TTFT p95, queue wait p95; burn-rate alerts
- [ ] 🔴 k6: load, spike, and soak tests; a capacity report
- [ ] 🔴 Chaos: toxiproxy latency on the LLM mock; kill pods; fail Postgres over
- [ ] ⚫ Reproduce a retry storm or metastable failure, then write a post-mortem

## 🧠 Cognitive tasks
- [ ] Pre-mortem before every Orbit version
- [ ] Write one blameless post-mortem per phase

## 🛰️ Orbit integration
- [ ] Chaos Day (W14) + Production Day (W18) boss fights

> [!info] Go deeper
> 🧩 [[Distributed & Cloud Patterns]] · [[Anti-Patterns & Code Smells]]

## Resources
- Google *SRE book* + *SRE Workbook* (free, sre.google) ⭐ · *Release It!* 2e ⭐
- *Systems Performance* 2e (Gregg) + brendangregg.com · *Implementing Service Level Objectives* (Hidalgo)
- Marc Brooker's blog (AWS) on retries, backoff, metastability ⭐
