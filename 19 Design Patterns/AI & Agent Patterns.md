---
tags: [patterns, ai, agents, llm]
---
# 🤖 AI & Agent Patterns

## A. Workflow patterns (deterministic control flow, LLM inside)
| Pattern | Structure | Use when | Orbit use case |
|---|---|---|---|
| **Augmented LLM** | LLM + retrieval + tools + memory | Base block | Everywhere |
| **Prompt chaining** | Step 1 → gate → step 2 … | Decomposable tasks | UC8 content pipeline, UC9 |
| **Routing** | Classify → specialized path/model | Distinct categories | UC1 triage, UC7 |
| **Parallelization: sectioning** | Independent subtasks in parallel | Speed, specialization | UC10 PR reviewers |
| **Parallelization: voting** | Same task N times → aggregate | Confidence, safety | UC12 guard |
| **Orchestrator–workers** | LLM plans subtasks dynamically → workers → synthesize | Unpredictable subtasks | UC4 research |
| **Evaluator–optimizer** | Generate → critique → refine (bounded loop) | Clear quality criteria | UC4, UC8 |
| **Map-reduce over documents** | Summarize chunks → combine | Long inputs | UC5, meeting notes |

## B. Agent patterns (the LLM controls the flow)
| Pattern | Notes | Orbit |
|---|---|---|
| **ReAct** | Think → act (tool) → observe → repeat | Go from-scratch agent |
| **Plan-and-execute** | Plan once, execute steps, re-plan on failure | UC6 analyst |
| **Reflection / self-critique** | Agent reviews its own output | UC4 |
| **Supervisor (hierarchical multi-agent)** | A manager routes to specialist agents | UC11 |
| **Handoffs / swarm** | Agents transfer control with context | UC1 → UC3 |
| **Human-in-the-loop** ⭐ | Approve / edit / reject tool calls; interrupt + resume | UC3, UC7, UC8 |
| **Durable agent** | Checkpoint every step; resume after a crash | LangGraph checkpointer, Orbit engine |
| **Tool-use loop with budgets** | Max steps/tokens/$, loop detection | All agents |

## C. Retrieval patterns
Naive RAG → **advanced RAG** (query rewrite, hybrid search, rerank, contextual chunks) → **agentic RAG** (the agent decides when/what to retrieve) → **corrective RAG** (grade retrieved docs, re-search if poor) → GraphRAG (entity graphs, awareness) · Parent-child chunks · Metadata/ACL filtering · Citations

## D. Memory & context patterns
Conversation buffer · **summary memory** (compact old turns) · vector memory (recall past facts) · entity/profile memory · scratchpad · **context compaction** · **tool-result truncation/summarization** · **stable prefix for prompt caching**

## E. Reliability, safety & cost patterns
| Pattern | What |
|---|---|
| **Structured output + validate + repair** | Schema → validate → re-ask with the error (≤ N) |
| **Guardrail sandwich** | Input guard → LLM → output guard |
| **Dual LLM / quarantine** ⭐ | A privileged LLM never sees untrusted text; a quarantined LLM processes it and returns only symbolic references (Simon Willison) |
| **Capability-scoped tools** | Least privilege per agent/tenant; no generic "run any SQL" |
| **Confirmation for side effects** | Irreversible tools require approval |
| **LLM-as-judge** | Rubric-based grading, calibrated against humans |
| **Model cascade / router** | Cheap model first; escalate on low confidence |
| **Fallback chain** | Provider A → B → cached/degraded answer |
| **Semantic cache** | Reuse answers for similar queries (measure false hits!) |
| **Idempotent tool calls** | Idempotency keys so retries don't double-act |
| **Prompt versioning + A/B** | Prompts are code: version, test, roll back |
| **Batch inference** | Offline jobs through batch APIs at lower cost |

## 🔬 Katas
- [ ] Implement all 6 workflow patterns as Orbit workflow definitions (JSON) with one eval each
- [ ] The same task (UC4) as (a) prompt chain, (b) orchestrator–workers, (c) autonomous agent → compare quality, cost, and latency in a table
- [ ] Dual-LLM pattern vs naive: run 20 indirect-injection docs through both
- [ ] Model cascade: find the confidence threshold that minimizes cost at ≥ 95% of the strong model's quality
