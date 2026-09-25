---
tags: [assignments, phase-5, ai]
weeks: W19–W22
---
# 📝 Assignments: Phase 5 (AI Engineering: all the use cases)

## W19 - LLM Engineering Deep Dive
**🎯 A19**
- [ ] Gateway v2: **routing policies** (by task/cost), **cascade** (cheap → strong on low confidence), provider fallback, **prompt caching** (stable prefix ordering), **semantic cache** with a measured false-hit rate, per-tenant **$ budgets**
- [ ] Prompt registry: versioned templates, variables, A/B assignment, linked eval scores
- [ ] **UC5**: document extraction: a `map` step over 500 PDFs/images (multimodal) → schema validation + business rules → low-confidence items go to a human review queue
- [ ] **UC8**: content pipeline: prompt chaining with gates + evaluator–optimizer (≤ 2 loops)
- **Acceptance:** UC5 field accuracy ≥ 95% on 50 labeled docs; cost per doc reported; the semantic cache's false-hit rate < 1% at the chosen threshold

**🔬 Lab (🔴):** Karpathy **minbpe** (or a toy BPE); measure TTFT vs prompt length and the effect of prompt caching ([[LLM Inference Internals]])
**🧠 Cognitive:** *Predict*: token counts and $ for 10 prompts (English, Hindi, JSON, code) → measure
**🌀 Open:** Design the cascade policy: which confidence signals can you trust? (logprobs, self-rating, verifier model, schema validity)
**Score:** __/28

## W20 - RAG Done Right
**🎯 A20** orbit-knowledge retrieval
- [ ] **Hybrid**: pgvector HNSW + Postgres FTS → **reciprocal rank fusion** → **reranker**
- [ ] Contextual chunk headers; parent-child chunks; metadata filters; **document ACLs** enforced at query time
- [ ] Multi-turn **query rewriting**; citations; "I don't know" when support is weak
- [ ] **Eval set**: 100 questions with gold passages → recall@5, MRR, faithfulness (LLM judge calibrated on 30 human labels)
- **UC2 full**: knowledge copilot
- **Acceptance:** recall@5 ≥ 0.85; faithfulness ≥ 0.9; an ACL test proves user A never receives user B's private chunks

**🔬 Lab (🔴):** **BM25 + simplified HNSW from scratch in Go**; compare recall and latency against pgvector on 100k vectors
**🧠 Cognitive:** error analysis: read 30 bad answers → categorize them (retrieval miss / chunking / ranking / generation) → fix the top category first
**🌀 Open:** Long context vs RAG for a 2M-token corpus: cost, latency, quality, freshness, ACLs
**Score:** __/28

## W21 - Agents, LangGraph & MCP
**🎯 A21**
- [ ] **ReAct agent from scratch in Go**: tool registry, a scratchpad, budgets (steps/tokens/$), **loop detection** (repeated tool+args), context compaction
- [ ] The **same agent in LangGraph** (Python): state graph, Postgres checkpointer, `interrupt` for approval, time travel, streaming
- [ ] **Orbit as an MCP server** (Spring AI): tools `list_workflows`, `start_run`, `get_run`, `search_knowledge`, `approve_step`; resources: definitions, run logs; test with MCP Inspector and a real client (Claude Desktop/Claude Code)
- [ ] **MCP client in orbit-tools**: register external MCP servers (GitHub, web search, filesystem, Prometheus) as scoped Orbit tools
- [ ] **UC4** research agent (orchestrator–workers + evaluator) · **UC10** PR review bot · **UC11** supervisor multi-agent
- **Acceptance:** UC4 finishes 20 prompts within budget; UC11 vs a single agent compared on quality/cost/latency in a table

**🔬 Lab:** LangChain Academy *Intro to LangGraph* modules 1–5
**🧠 Cognitive:** "What did the framework hide?": list 10 things LangGraph does that your Go agent had to do by hand
**🌀 Open:** A tool permission model: per-tenant, per-agent, and per-user scopes; approval policies; audit. Design it
**Score:** __/28

## W22 - Evals, Guardrails & the Red-Team Boss Fight
**🎯 A22**
- [ ] **orbit-evals**: suites per use case (code checks + LLM-as-judge), a promptfoo/DeepEval runner, a **CI gate** on PRs that touch prompts/models/tools, online sampling of 5% of production runs
- [ ] Guardrails: injection detector (**UC12** voting guard), **dual-LLM/quarantine** for untrusted content, output schema validation, PII redaction, tool allowlists
- [ ] **UC6** text-to-SQL analyst (read-only role, allowlisted tables, LIMIT, timeout, self-verification) · **UC7** SRE agent via Prometheus/K8s MCP with approval gates
- [ ] Langfuse (or OTel-native) traces of every LLM/tool call

**⚫ Phase boss fight: Red-Team Day.** Attack your own agents with 30+ attacks: direct/indirect prompt injection (in docs, tool outputs, web pages), data exfiltration via tools, excessive agency, SQL tricks, cost-exhaustion loops. Fix, re-run, and publish a report with before/after numbers
**🧠 Cognitive:** *Transfer*: which classic security principles (least privilege, input validation, defense in depth, audit) map to which agent defenses?
**Score:** __/28
