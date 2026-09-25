---
tags: [ai, llm]
phase: 5
---
# 🧬 LLM Fundamentals

## Concepts (intuition-level, enough to reason about behavior)
- [ ] Tokens & tokenization (BPE); why cost and limits are in tokens
- [ ] Embeddings & vector similarity (cosine, dot product)
- [ ] Transformer intuition: attention, next-token prediction, pre-training vs post-training (SFT, RLHF/RLAIF)
- [ ] Sampling: temperature, top-p, max tokens, stop sequences
- [ ] Context windows, the "lost in the middle" effect, prompt caching
- [ ] Hallucinations and why they happen; grounding
- [ ] Reasoning / extended-thinking models: when the extra latency and cost are worth it
- [ ] Model selection: large vs small, open-weights vs API, latency vs quality vs cost
- [ ] Multimodal inputs (images, PDFs, audio)

## Integration skills
- [ ] Chat APIs (messages, roles, system prompts), **streaming** (SSE)
- [ ] **Structured output** (JSON schema), validation, retries on invalid output
- [ ] **Tool / function calling**: the loop (model → tool call → your code → result → model)
- [ ] Prompt caching, batching APIs for offline jobs
- [ ] Rate limits, timeouts, retries with backoff, fallbacks across models/providers
- [ ] Token and cost accounting per request/user/feature
- [ ] Local models with **Ollama** for dev/testing; serving with vLLM (awareness)

## Prompt / context engineering
- [ ] Clear instructions, role, context, examples (few-shot), output format
- [ ] XML tags / sectioning, chain-of-thought where appropriate
- [ ] Prompt templates versioned in code, tested with evals

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 Call hosted + local (Ollama) models from Java, Go, and Python; compare the ergonomics
- [ ] 🟡 Structured extraction with schema validation + a repair loop (UC1/UC5)
- [ ] 🔴 Measure TTFT vs prompt length, ITL vs load, and the effect of prompt caching
- [ ] ⚫ Karpathy's minbpe / *Let's build GPT*

## 🧠 Cognitive tasks
- [ ] Predict token counts and cost before every experiment
- [ ] First-principles: why does output length dominate latency?

## 🛰️ Orbit integration
- [ ] orbit-llm-gateway v1 → v2

> [!info] Go deeper
> ⚙️ [[LLM Inference Internals]] · 🧩 [[AI & Agent Patterns]]

