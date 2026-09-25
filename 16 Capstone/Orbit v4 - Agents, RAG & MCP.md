---
tags: [capstone, orbit, ai]
version: v4
weeks: W19–W22
---
# Orbit v4: Agents, RAG, MCP, Evals & Guardrails (Phase 5)

## Scope
### LLM gateway v2
- [ ] Model routing policies (cheap → strong cascade), provider fallback, **prompt caching** (stable prefixes), **semantic cache** (embedding similarity + measured false-hit rate), per-tenant **budgets** ($), PII redaction hook

### RAG (orbit-knowledge)
- [ ] Hybrid retrieval: pgvector HNSW + Postgres FTS (BM25-like) → **reciprocal rank fusion** → **reranker**
- [ ] Contextual chunk headers, parent-child chunks, metadata filters, **document ACLs** enforced at query time
- [ ] Citations; "I don't know" behavior; query rewriting for multi-turn chat

### Agents
- [ ] **ReAct agent loop from scratch in Go** (no framework): tool registry, budgets (steps/tokens/$), loop detection, scratchpad compaction
- [ ] **LangGraph runtime (Python)**: plan-and-execute, supervisor multi-agent, Postgres checkpointer, `interrupt` for HITL, time travel
- [ ] Memory: thread memory (summarized), long-term memory store (per user), tool-result truncation

### MCP
- [ ] **Orbit as an MCP server** (Spring AI): tools `list_workflows`, `start_run`, `get_run`, `search_knowledge`, `approve_step`; resources: workflow definitions, run logs; OAuth for remote HTTP transport
- [ ] **MCP client in orbit-tools**: connect external MCP servers (GitHub, Slack, filesystem, web search, Prometheus) as Orbit tools, with per-tenant scopes and approval policies

### Evals & guardrails
- [ ] orbit-evals: datasets, suites per use case, code checks + LLM-as-judge (validated on human labels), **CI gate on prompt/model changes**, online sampling
- [ ] Guardrails: injection detection (UC12 voting guard), **dual-LLM / quarantine pattern** for untrusted content, output schema validation, allow-listed tool scopes, PII redaction
- [ ] Langfuse (or OTel-native) traces for every LLM/tool call

## Use cases shipped
UC2 (full RAG) · UC4 · UC5 · UC6 · UC7 · UC8 · UC10 · UC11 · UC12 → see [[Orbit - Use Cases]]

## Definition of done
- [ ] Eval dashboard with before/after numbers for every RAG/agent improvement
- [ ] **Red-team report**: 30+ injection/jailbreak/tool-abuse attempts, results, and fixes
- [ ] Cost per run per use case; a 40% cost reduction via routing + caching, with quality held
- [ ] Demo video (3 min): build a workflow in the UI → run → approve → trace → eval
