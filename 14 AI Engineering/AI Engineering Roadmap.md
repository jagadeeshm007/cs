---
tags: [ai, roadmap, moc]
phase: 5
---
# 🤖 AI Engineering Roadmap (2026)

> [!important] Positioning
> Most companies don't need you to train models. They need engineers who can **build reliable, secure, cost-efficient products on top of LLMs**. That is software engineering + distributed systems + evaluation discipline. Your backend depth is your edge.

## Layers (core → advanced)
1. **Foundations**: [[LLM Fundamentals]]: tokens, embeddings, transformers intuition, sampling, context windows, limitations
2. **Integration**: API calls, streaming, structured output, tool calling, retries/timeouts, cost tracking ([[Spring AI]], Go/Python SDKs)
3. **Context engineering**: prompts, system prompts, few-shot examples, managing long context, memory
4. **Retrieval**: [[RAG]]: chunking, embeddings, vector + hybrid search, reranking, citations, GraphRAG (awareness)
5. **Workflows & agents**: [[Agents & Workflows]] · [[LangChain & LangGraph]]: chains → routers → orchestrator-workers → autonomous agents; human-in-the-loop; durable execution
6. **Interoperability**: [[MCP]] (tools/resources/prompts), A2A (agent-to-agent protocol)
7. **Production**: [[Evals, Guardrails & LLMOps]]: evals, tracing, guardrails, prompt-injection defense, LLM gateways, semantic caching, cost/latency optimization
8. **Emerging**: multimodal (vision, voice/realtime APIs), computer use / browser agents, small/local models (Ollama, vLLM), fine-tuning (LoRA) awareness, reasoning models and "thinking" budgets, AI coding agents in the SDLC

## AI-native engineering habits (use AI to become a better engineer)
- Use AI coding assistants (Claude Code, Cursor, Copilot) daily, but **review every line**. Interviewers still test whether *you* understand
- Use AI to generate test cases, explain unfamiliar code, and critique your designs, then verify with docs
- Never outsource the learning loop: solve the DSA problem first, then ask the AI for a critique

## LLM system design questions to practise
- Design an enterprise RAG search over 10M documents with access control
- Design a customer-support agent that can take actions (refunds) safely
- Design an LLM gateway for 50 internal teams (routing, quotas, caching, observability, PII redaction)
- Design an evaluation platform for prompts/agents

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟡 All 12 Orbit use cases (UC1–UC12) with an eval suite each
- [ ] 🔴 The same task as a chain vs orchestrator–workers vs an autonomous agent: a quality/cost/latency table
- [ ] ⚫ Red-Team Day + a 40% cost cut with quality held

## 🧠 Cognitive tasks
- [ ] Every AI feature starts with: "What's the simplest pattern that works, and how will I measure it?"

## 🛰️ Orbit integration
- [ ] [[Orbit v4 - Agents, RAG & MCP]]

> [!info] Go deeper
> ⚙️ [[LLM Inference Internals]] · 🧩 [[AI & Agent Patterns]] · 🛰️ [[Orbit - Use Cases]]

## Resources
- ⭐ *AI Engineering* (Chip Huyen) · *Hands-On Large Language Models* (Alammar & Grootendorst)
- ⭐ Anthropic: "Building effective agents", prompt engineering guide, tool use docs, "Effective context engineering for AI agents"
- LangChain Academy (free) · DeepLearning.AI short courses (free) · modelcontextprotocol.io
- Karpathy: *Neural Networks: Zero to Hero*, *Let's build GPT*, *Intro to LLMs* ⭐
- 3Blue1Brown: neural networks / transformers series
- Blogs: Eugene Yan, Hamel Husain, Simon Willison, Chip Huyen, Lilian Weng
