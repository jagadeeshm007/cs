---
tags: [ops, observability]
phase: 4
---
# 🔭 Observability

## Core → Advanced
- [ ] Monitoring vs observability; the three pillars (+ profiles, events)
- [ ] **Structured logging** (JSON), log levels, correlation/trace IDs in every log line; what NOT to log (PII, secrets)
- [ ] **Metrics**: counters, gauges, histograms; RED/USE; percentiles from histograms; **cardinality** pitfalls ⭐
- [ ] **Distributed tracing**: spans, context propagation (W3C `traceparent`), sampling (head vs tail)
- [ ] **OpenTelemetry** ⭐: SDKs (Java agent auto-instrumentation, Go SDK), the Collector (receivers → processors → exporters), OTLP
- [ ] Stack: **Prometheus** (PromQL), **Grafana**, **Loki** (logs), **Tempo** (traces), Pyroscope (continuous profiling), Alertmanager
- [ ] Alerting: alert on symptoms (SLO burn rate), not causes; runbooks; avoid alert fatigue
- [ ] Dashboards: service overview (RED), dependency dashboards, business KPIs
- [ ] eBPF-based observability (awareness): Cilium Hubble, Pixie, Grafana Beyla
- [ ] LLM observability → [[Evals, Guardrails & LLMOps]]

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 The LGTM stack (Loki, Grafana, Tempo, Mimir/Prometheus) + an OTel Collector via Compose
- [ ] 🟡 One trace across Java → Go → Kafka → Go → the LLM provider
- [ ] 🔴 **A mini tracer in Go** with W3C propagation over HTTP + Kafka (W17 lab)
- [ ] 🔴 GenAI spans: model, tokens, cost; per-tenant cost dashboards
- [ ] ⚫ Tail sampling that keeps 100% of errors and slow traces at 5% overall volume

## 🧠 Cognitive tasks
- [ ] Symptom → hypotheses using only dashboards (drill prompts in [[Cognitive Drills]])

## 🛰️ Orbit integration
- [ ] Observability for [[Orbit v3 - Cloud Native]] + LLM tracing in v4

> [!info] Go deeper
> ⚙️ [[Envoy Internals]] · [[Kafka Internals]]

## Resources
- *Observability Engineering* (Majors, Fong-Jones, Miranda) ⭐ · opentelemetry.io docs · Grafana docs · *Prometheus: Up & Running*
