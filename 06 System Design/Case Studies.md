---
tags: [system-design, practice]
---
# 📋 System Design Case Studies

Do each one with the *System Design Case* template: 45-min timed attempt → compare with references → note gaps → redo in 2 weeks.

## Tier 1: classics (W10–W12)
- [ ] URL shortener (IDs, redirects, caching, analytics)
- [ ] Rate limiter (distributed, algorithms)
- [ ] Key-value store / distributed cache
- [ ] Notification system (multi-channel, retries, preferences)
- [ ] News feed / timeline (fan-out on write vs read, celebrities)
- [ ] Web crawler

## Tier 2: product systems (W12–W14)
- [ ] Chat system (WhatsApp/Slack): presence, delivery receipts, ordering
- [ ] **Ticket booking (BookMyShow/Ticketmaster)**: seat contention, flash sales, virtual waiting room
- [ ] Ride sharing (Uber): geo-indexing, matching, location updates
- [ ] Food delivery (Swiggy/Zomato): dispatch, ETAs, order state machine
- [ ] E-commerce checkout + inventory (Flipkart/Amazon): reservations, sale spikes
- [ ] Payment system: idempotency, ledger (double-entry), reconciliation
- [ ] Video streaming (YouTube/Netflix): upload pipeline, transcoding, CDN, adaptive bitrate

## Tier 3: advanced (W14+, company-specific)
- [ ] Google Docs (OT/CRDT collaborative editing)
- [ ] Distributed job scheduler (cron at scale)
- [ ] Search autocomplete / typeahead
- [ ] Top-K / trending (streaming, count-min sketch)
- [ ] Ad click aggregation (stream processing, exactly-once)
- [ ] Metrics/monitoring system (time series)
- [ ] Distributed message queue (design Kafka)
- [ ] Dropbox/Google Drive (chunking, dedupe, sync)
- [ ] Proximity service / Yelp (geohash, quadtree)
- [ ] **LLM-powered systems**: ChatGPT-like chat service, enterprise RAG search, AI agent platform, LLM gateway

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟡 1 case per week, timed at 45 min, using the *System Design Case* template
- [ ] 🔴 Redo each case after 2 weeks **without notes**; compare versions
- [ ] ⚫ Record a mock and grade yourself on structure, trade-offs, depth, and communication

## 🧠 Cognitive tasks
- [ ] Constraint flip on every case: 100× scale, strong consistency, multi-region
- [ ] Reverse engineering: read the real company's engineering blog after your attempt; list 3 gaps

## 🛰️ Orbit integration
- [ ] **Your capstone is a case study**: "Design an AI workflow platform", "Design an LLM gateway", "Design a durable workflow engine (Temporal)", "Design a RAG platform with ACLs"

> [!info] Go deeper
> 🧩 [[Distributed & Cloud Patterns]] · [[AI & Agent Patterns]]

