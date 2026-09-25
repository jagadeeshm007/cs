---
tags: [ai, evals, llmops, security]
phase: 5
---
# 🧪 Evals, Guardrails & LLMOps

> [!quote] "If you're not evaluating, you're guessing." Evals are to LLM apps what tests are to code.

## Evals
- [ ] Error analysis first: read 50–100 real traces and categorize the failures (Hamel Husain's method) ⭐
- [ ] Eval types: code-based assertions, **LLM-as-judge** (with a rubric, validated against human labels), human review
- [ ] Datasets: golden sets, synthetic data generation, production samples
- [ ] Metrics: task success, faithfulness, relevance, tool-call accuracy, latency, cost
- [ ] Run evals in CI on every prompt/model change (regression testing)
- [ ] Online evals + A/B tests in production
- [ ] Tools: promptfoo, DeepEval, Ragas, LangSmith, **Langfuse** (open source) ⭐, Braintrust, Arize Phoenix

## Guardrails & security
- [ ] **Prompt injection** (direct + indirect via retrieved docs/tool output): defense in depth, least privilege, human confirmation, input/output filters
- [ ] PII detection/redaction; content moderation
- [ ] Output validation (schemas), hallucination checks, refusal handling
- [ ] OWASP Top 10 for LLM apps

## LLMOps / production
- [ ] Tracing every call (inputs, outputs, tokens, latency, cost) with OpenTelemetry GenAI semantic conventions / Langfuse
- [ ] **LLM gateway**: provider routing/fallback, rate limits, per-team quotas, key management, caching (LiteLLM, Envoy AI Gateway, Kong AI Gateway)
- [ ] **Semantic caching** (embedding similarity) vs exact caching; prompt caching
- [ ] Cost optimization: smaller models for easy steps, routing by difficulty, batching, context trimming
- [ ] Latency: streaming, parallel tool calls, speculative/prefetch, smaller models
- [ ] Prompt/version management and rollbacks

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟡 Golden datasets for UC1/UC2/UC5 + code-based checks
- [ ] 🔴 An LLM-as-judge calibrated against 30 human labels (report agreement)
- [ ] 🔴 A CI eval gate + online sampling + dashboards
- [ ] ⚫ **Red-Team Day**: 30+ attacks, fixes, before/after report

## 🧠 Cognitive tasks
- [ ] Error analysis first: read 50 traces before writing any metric

## 🛰️ Orbit integration
- [ ] The orbit-evals service; guardrail steps in every workflow

> [!info] Go deeper
> 🧩 [[AI & Agent Patterns]] · [[Anti-Patterns & Code Smells]]

