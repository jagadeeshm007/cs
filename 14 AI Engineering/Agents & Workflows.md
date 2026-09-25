---
tags: [ai, agents, workflows]
phase: 5
---
# 🕹️ Agents & Workflows

## Workflows vs agents (Anthropic's "Building effective agents" taxonomy)
| Pattern | What | Use when |
|---|---|---|
| Augmented LLM | LLM + retrieval + tools + memory | Base building block |
| Prompt chaining | Fixed sequence of steps | Decomposable tasks, with gates between steps |
| Routing | Classify, then send to a specialized path | Distinct input categories |
| Parallelization | Sectioning / voting | Speed or confidence |
| Orchestrator–workers | LLM breaks down work dynamically | Unpredictable subtasks |
| Evaluator–optimizer | Generate → critique → refine | Clear evaluation criteria |
| **Autonomous agent** | LLM in a loop with tools and environment feedback | Open-ended problems where some autonomy is acceptable |

> [!tip] Start with the simplest thing that works. Add agency only when it measurably helps.

## Engineering concerns
- [ ] Tool design: clear names/descriptions, typed inputs, idempotent, least privilege, good error messages
- [ ] Loop control: max steps, budgets (tokens/time/$), stop conditions
- [ ] State & memory: short-term (thread), long-term (store), summarization
- [ ] **Human-in-the-loop** for irreversible actions (payments, emails, deletes) ⭐
- [ ] **Durable execution**: agents as long-running workflows (**Temporal**, LangGraph checkpoints); retries without double side effects
- [ ] Multi-agent: supervisor, handoffs, **A2A protocol** for cross-agent interop (awareness)
- [ ] Security: prompt injection via tool results, sandboxing code execution, excessive agency
- [ ] Observability: trace every step, tool call, and token

## Workflow engines (non-AI too; very valuable backend skill)
- [ ] **Temporal** (Go/Java SDKs): workflows, activities, retries, signals, versioning ⭐
- [ ] Step Functions / Airflow / Camunda (awareness)

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟡 All 6 workflow patterns as Orbit workflow definitions
- [ ] 🔴 A **ReAct agent from scratch in Go** with budgets and loop detection
- [ ] 🔴 A durable agent: kill the worker mid-agent → resume from the checkpoint without repeating side effects
- [ ] ⚫ Temporal vs Orbit engine vs LangGraph for the same agent; write the ADR

## 🧠 Cognitive tasks
- [ ] Pre-mortem for autonomous agents: 10 failure modes + mitigations

## 🛰️ Orbit integration
- [ ] UC3, UC4, UC6, UC7, UC11 in [[Orbit - Use Cases]]

> [!info] Go deeper
> 🧩 [[AI & Agent Patterns]] · [[Distributed & Cloud Patterns]]

