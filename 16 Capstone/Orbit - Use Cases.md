---
tags: [capstone, orbit, ai, use-cases]
---
# 🧩 Orbit: Use Cases & Reference Apps

Every AI pattern you need to know is built as a **reference app on top of Orbit**. Each one is a workflow definition + tools + prompts + an eval suite.

## Coverage matrix
| # | Reference app | Structured output | Tool calling | RAG | Workflow pattern | Agent | HITL | MCP | Multimodal | Trigger | Version |
|---|---|---|---|---|---|---|---|---|---|---|---|
| UC1 | Support ticket triage | ✅ | ✅ | | Routing | | | | | API | v1 |
| UC2 | Knowledge copilot (chat over docs) | | | ✅ | Augmented LLM + memory | | | | | Chat | v1 → v4 |
| UC3 | Refund agent with approvals | ✅ | ✅ | ✅ | Saga + compensation | ✅ | ✅ | | | API | v2 |
| UC4 | Research agent | | ✅ | ✅ | Orchestrator–workers + evaluator–optimizer | ✅ | | ✅ web search | | API | v4 |
| UC5 | Document extraction pipeline | ✅ | | | Map (fan-out) + validation retry | | review queue | | ✅ PDFs/images | Cron + S3 upload | v4 |
| UC6 | Data analyst (text-to-SQL) | ✅ | ✅ SQL tool | schema RAG | Plan → execute → verify | ✅ | | | charts | Chat | v4 |
| UC7 | SRE / DevOps agent | | ✅ | runbook RAG | Routing + agent | ✅ | ✅ | ✅ Prometheus/K8s | | Alertmanager webhook | v4 |
| UC8 | Content pipeline | ✅ | | ✅ brand guide | Prompt chaining + gates + evaluator–optimizer | | ✅ | | | API | v4 |
| UC9 | Meeting notes → actions | ✅ | ✅ | | Chaining | | | ✅ Slack/Jira | audio (stretch) | Webhook | v2 |
| UC10 | PR review bot | ✅ | ✅ | ✅ code conventions | Parallelization (sectioning) | ✅ | | ✅ GitHub | | GitHub webhook | v4 |
| UC11 | Multi-agent planner | | ✅ | ✅ | Supervisor / handoffs | ✅✅ | ✅ | ✅ | | API | v4 |
| UC12 | Voting classifier (safety/moderation) | ✅ | | | Parallelization (voting) | | | | ✅ images | Inline guard | v4 |

## Use-case specs
### UC1 · Support ticket triage (v1)
Input: raw ticket text/email → **classify** (category, priority, sentiment) with a JSON schema → **extract** (order ID, product, customer) → **route**: bug → create a GitHub issue (tool); billing → hand off to UC3; how-to → answer with UC2.
- Acceptance: ≥ 90% category accuracy on a 100-ticket labeled set; invalid JSON repaired within 1 retry; p95 < 3 s

### UC2 · Knowledge copilot (v1 chat → v4 RAG)
Chat over a tenant's docs, with citations, ACL-aware retrieval, conversation memory (summarized after N turns), and streaming.
- Acceptance: recall@5 ≥ 0.85 on 100 questions; faithfulness ≥ 0.9 (judge validated against human labels); says "I don't know" when retrieval is empty

### UC3 · Refund agent with approvals (v2)
Agent reads order history (tool) → checks policy (RAG) → proposes a refund → **human approval** (inbox, 24h timeout → escalate) → calls the payment tool → notifies the customer; on failure, **compensates** (reverse the ledger entry, reopen the ticket).
- Acceptance: kill workers mid-run 100× → no double refunds; every refund has an approver audit trail

### UC4 · Research agent (v4)
Planner splits a question into 3–6 sub-questions → **parallel sub-agents** do web search (MCP) + reading → synthesizer writes a cited report → **evaluator** scores coverage/citations → revise ≤ 2 loops.
- Acceptance: token budget enforced; loop detection; report quality judged ≥ 4/5 on 20 prompts

### UC5 · Document extraction pipeline (v4)
Upload invoices/resumes (PDF/image) → multimodal extraction → schema validation + business rules → low-confidence items go to a **human review queue** → store to Postgres. Runs a `map` step over 500 docs with bounded concurrency; nightly cron.
- Acceptance: field-level accuracy ≥ 95% on 50 labeled docs; resumable after a crash; cost per doc reported

### UC6 · Data analyst, text-to-SQL (v4)
Question → retrieve relevant table schemas (RAG over the catalog) → generate SQL → **read-only role + allowlisted tables + LIMIT + timeout** → execute on ClickHouse → self-check the result → answer with a chart spec.
- Acceptance: 80% execution accuracy on 50 questions; zero writes possible (prove it with attack prompts)

### UC7 · SRE agent (v4)
Alertmanager webhook → gather context via MCP (Prometheus queries, K8s events, recent deploys) → RAG over runbooks → hypothesis + proposed action → **approval** before any mutating action (e.g. rollout restart).
- Acceptance: correct root-cause category in 7/10 injected incidents from your chaos drills

### UC8 · Content pipeline (v4)
Brief → outline → **gate** (checks structure) → draft → critique (evaluator) → revise → brand-style check (RAG over the style guide) → human approval → publish via webhook.

### UC9 · Meeting notes → action items (v2)
Webhook with a transcript → summarize → extract action items (owner, due date) → create tasks via Jira/Slack tools (MCP) → post a summary. Idempotent on webhook retries.

### UC10 · PR review bot (v4)
GitHub webhook → fetch the diff (GitHub MCP) → **parallel reviewers** (security, performance, style) → aggregate → post comments. Rate-limited per repo; conventions retrieved from the repo's docs.

### UC11 · Multi-agent planner (v4)
Supervisor agent delegates to researcher, coder (code-exec sandbox), and critic agents; shared state in LangGraph; human checkpoint before the final action. Compare quality and cost against a single agent.

### UC12 · Voting classifier / guardrail (v4)
3 parallel cheap-model votes (or 1 cheap + 1 strong) for moderation / prompt-injection detection; used as an inline guard step by other workflows.

## Platform capabilities checklist (what Orbit itself must support)
- [ ] Step types: `llm`, `tool`, `http`, `code`, `rag.search`, `agent`, `branch`, `map`, `parallel`, `human`, `wait/timer`, `subworkflow`
- [ ] Expression language for conditions/mappings (`{{ steps.classify.output.priority == "high" }}`)
- [ ] Prompt registry with versions + A/B + eval scores
- [ ] Tool registry: JSON Schema inputs, auth, scopes, "requires approval" flag, timeouts, idempotency
- [ ] Triggers: API, cron, webhook, Kafka, S3 upload
- [ ] Run timeline + trace viewer (every LLM call, tool call, token count, cost)
- [ ] Budgets and quotas per tenant/workflow; model routing policies
- [ ] Evals: datasets, suites, judges, CI gate, online sampling
- [ ] Guardrails: input/output validators, PII redaction, injection detection, allow/deny lists
