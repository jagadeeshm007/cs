---
tags: [ai, langchain, langgraph]
phase: 5
---
# 🦜 LangChain & LangGraph

> [!note] Mental model
> **LangChain** = integrations + building blocks (models, prompts, retrievers, tools). **LangGraph** = a low-level framework for **stateful, controllable agent workflows as graphs**, with persistence, streaming, and human-in-the-loop. In 2026, use LangGraph for anything agentic. Python is the most mature; LangGraph.js exists; in Java, see LangChain4j / Spring AI.

## LangChain
- [ ] Chat models, messages, prompt templates, output parsers / structured output
- [ ] Tools (`@tool`), tool-calling models
- [ ] Retrievers, document loaders, text splitters, vector store integrations
- [ ] Runnables / LCEL composition (awareness)

## LangGraph ⭐
- [ ] `StateGraph`: state schema, nodes, edges, **conditional edges**, reducers
- [ ] Prebuilt ReAct agent vs a custom graph
- [ ] **Persistence / checkpointers** (Postgres checkpointer), threads, memory (short-term vs long-term store)
- [ ] **Human-in-the-loop**: `interrupt`, approve/edit tool calls, time travel
- [ ] Streaming (tokens, updates, events)
- [ ] Subgraphs, multi-agent patterns (supervisor, swarm/handoffs)
- [ ] Deployment options (LangGraph Platform / self-host with FastAPI), LangSmith tracing
- [ ] Connecting to MCP servers (MCP adapters)

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 LangChain Academy *Intro to LangGraph* modules 1–2
- [ ] 🟡 A state graph with conditional edges + a Postgres checkpointer
- [ ] 🔴 `interrupt` for approvals + time travel + streaming to orbit-stream
- [ ] ⚫ A supervisor multi-agent (UC11) invoked as an Orbit `agent` step

## 🧠 Cognitive tasks
- [ ] "What did the framework hide?": compare it with your Go ReAct agent

## 🛰️ Orbit integration
- [ ] The orbit-agents service

> [!info] Go deeper
> 🧩 [[AI & Agent Patterns]] · 🤖 [[Agents & Workflows]]

## Resources
- langchain-ai.github.io/langgraph · python.langchain.com · LangChain Academy · LangChain YouTube
