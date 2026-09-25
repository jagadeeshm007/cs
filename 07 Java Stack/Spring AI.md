---
tags: [java, spring, ai]
phase: 5
---
# 🤖 Spring AI (+ LangChain4j)

## Checklist
- [ ] `ChatClient` fluent API, system/user messages, prompt templates
- [ ] Model portability: Anthropic, OpenAI, Gemini, Ollama (local), Bedrock
- [ ] Streaming responses (Flux → SSE)
- [ ] **Structured output** → Java records
- [ ] **Tool calling** (`@Tool` methods) and returning tool results
- [ ] Advisors: chat memory, RAG (`QuestionAnswerAdvisor`), logging, safeguards
- [ ] `VectorStore` abstraction: **pgvector**, Redis, etc.; ETL pipeline (DocumentReader → splitter → embed → store)
- [ ] **MCP**: Spring AI MCP server & client starters ⭐ → [[MCP]]
- [ ] Observability: Micrometer metrics for tokens and latency
- [ ] Evaluation helpers (relevancy/fact-checking evaluators)
- [ ] Compare with **LangChain4j** (AI Services, agents) and know when you'd pick each

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 `ChatClient` with streaming + structured output into records
- [ ] 🟡 `@Tool` methods + advisors (memory, logging); compare with LangChain4j AI Services
- [ ] 🔴 An ETL pipeline into pgvector + `QuestionAnswerAdvisor`, then replace it with your own hybrid retriever
- [ ] 🔴 **Orbit MCP server** with the Spring AI MCP starter (tools + resources + OAuth)
- [ ] ⚫ The MCP client side: connect external MCP servers as Orbit tools with scopes

## 🧠 Cognitive tasks
- [ ] Framework vs hand-rolled: what does Spring AI's tool calling do that your Go loop does by hand?

## 🛰️ Orbit integration
- [ ] orbit-knowledge (RAG) and orbit-tools (MCP server/client) → [[Orbit v4 - Agents, RAG & MCP]]

> [!info] Go deeper
> ⚙️ [[LLM Inference Internals]] · 🧩 [[AI & Agent Patterns]] · 🤖 [[MCP]]

## Resources
- docs.spring.io/spring-ai ⭐ · Spring AI examples repo · Dan Vega + Josh Long videos on Spring AI · docs.langchain4j.dev
Related: [[AI Engineering Roadmap]]
