---
tags: [capstone, orbit]
version: v1
weeks: W5–W9
---
# Orbit v1: Core Platform (Phase 2)

## Scope
- [ ] **orbit-api (Spring Boot 4, Spring Modulith)**: modules `tenancy`, `workflows`, `prompts`, `tools`, `runs`; versioned workflow definitions validated against JSON Schema; Flyway; ProblemDetail; OpenAPI
- [ ] **Multi-tenancy**: Keycloak (orgs/realms), JWT resource server, API keys (hashed, prefix lookup), **Postgres RLS** for tenant isolation
- [ ] **Idempotency-key starter** (custom Spring Boot starter backed by Redis)
- [ ] **orbit-llm-gateway v1 (Go)**: provider adapters (Anthropic, OpenAI, Ollama) behind a Strategy interface; streaming SSE passthrough; timeouts, retries, fallback; token counting; **per-tenant token bucket in Redis Lua**; exact-match cache
- [ ] **orbit-worker v1 (Go)**: executes `llm`, `tool`, `http`, `branch` steps from orbit-dag; the **tool-calling loop** (model → tool_use → execute → tool_result → model) with max iterations, per-tool timeout, output truncation
- [ ] **Tool registry**: JSON-Schema tool definitions; built-in tools: `http_request`, `sql_readonly`, `calculator`, `github_create_issue`
- [ ] **gRPC** between orbit-api (Java) and engine/worker (Go) with **buf**
- [ ] **GraphQL** for the UI: workflows → versions → runs → steps (DataLoader / `@BatchMapping`)
- [ ] **orbit-stream (Go)**: SSE for tokens + run events via Redis pub/sub; `Last-Event-ID` resume
- [ ] **orbit-web**: playground (chat + streaming), run timeline, workflow JSON editor
- [ ] Docker Compose for everything; GitHub Actions CI (Java + Go matrices)

## Use cases shipped
UC1 Support triage · UC2 v0 (chat + memory, no RAG yet)

## ADRs
ADR-001 Modular monolith control plane · ADR-002 Go data plane · ADR-003 Tenant isolation via RLS · ADR-004 Workflow definition format (JSON DSL vs code) · ADR-005 Gateway quota algorithm

## Definition of done
- [ ] 200 concurrent streaming chats without errors; p99 time-to-first-token overhead of the gateway < 30 ms
- [ ] Cross-tenant access attempts all fail (automated test suite)
- [ ] Blog: "Building an LLM gateway in Go: streaming, quotas, and fallbacks"
