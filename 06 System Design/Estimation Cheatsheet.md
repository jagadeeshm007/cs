---
tags: [system-design, cheatsheet]
---
# 🧮 Estimation Cheatsheet (back-of-the-envelope)

## Powers & time
- 2^10 ≈ 1 thousand (KB), 2^20 ≈ 1 million (MB), 2^30 ≈ 1 billion (GB), 2^40 ≈ 1 trillion (TB)
- 1 day ≈ 86,400 s ≈ **10^5 s**. 1 month ≈ 2.5 × 10^6 s. 1 year ≈ 3 × 10^7 s
- 1M requests/day ≈ **12 QPS** average. Peak ≈ 2–5× average (10×+ for flash sales)

## Rough capacities (per node, order of magnitude)
| Component | Throughput |
|---|---|
| Stateless app server (simple API) | 1k–10k RPS |
| PostgreSQL (simple indexed reads, good hardware) | 10k–50k QPS; writes ~5k–20k TPS |
| Redis | 100k+ ops/s |
| Kafka broker | 100s of MB/s |
| Single SSD | 100k+ IOPS |
| 1 Gbps network | ~125 MB/s |

## Sizes
- UUID 16 B · long 8 B · timestamp 8 B · typical row 100 B–1 KB · tweet ~300 B · image ~200 KB–2 MB · 1 min video (720p) ~50 MB

## Availability
| SLA | Downtime/year | Downtime/month |
|---|---|---|
| 99% | 3.65 days | 7.2 h |
| 99.9% | 8.76 h | 43.8 min |
| 99.99% | 52.6 min | 4.4 min |
| 99.999% | 5.26 min | 26 s |
Serial dependencies multiply: 99.9% × 99.9% = 99.8%.

## Template
1. DAU → actions/user/day → requests/day → ÷10^5 → avg QPS → × peak factor
2. Read:write ratio
3. Storage = objects/day × size × retention (× replication factor 3)
4. Bandwidth = QPS × payload
5. Cache = 20% of hot daily data (80/20 rule)
6. Servers ≈ peak QPS ÷ per-server QPS (+ headroom 30–50%)

Latency numbers: see [[Optimization Principles]].

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 Daily 5-min Fermi drill (log it in the drill log)
- [ ] 🟡 Estimate, then measure: Orbit's DB growth per 1M runs; tokens/day per tenant

## 🧠 Cognitive tasks
- [ ] Explain which estimate actually changed a design decision (most don't!)

## 🛰️ Orbit integration
- [ ] Capacity plan for [[Orbit v5 - Scale & Polish]]

> [!info] Go deeper
> 🧠 [[Cognitive Drills]]

