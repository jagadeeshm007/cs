---
tags: [assignments, phase-2]
weeks: W5–W9
---
# 📝 Assignments: Phase 2 (Backend + first AI features)

## W5 - Control Plane Skeleton + Mini DI Container
**🎯 A5** orbit-api skeleton ([[Orbit v1 - Core Platform]])
- [ ] Gradle multi-module; Spring Modulith modules `tenancy`, `workflows`, `prompts`, `tools`, `runs` with **module boundary tests**
- [ ] Workflow definitions: create a draft → validate against JSON Schema → **publish immutable versions**
- [ ] Flyway, ProblemDetail errors, OpenAPI, Testcontainers, ArchUnit (the domain must not depend on Spring/JPA)
- **Acceptance:** `./gradlew check` green; publishing the same version twice → 409

**🔬 Lab (🔴): Mini DI container in Java**: classpath scan for `@Component`, constructor injection, singleton scope, cycle detection with a readable error, `@PostConstruct`, and a **JDK dynamic proxy** for a `@Timed` annotation. Then explain how Spring does each of these ([[Spring Internals]])
**🧠 Cognitive:** step through `refresh()` in the debugger; draw the sequence from memory the next day
**🌀 Open:** Workflow definitions as JSON documents (jsonb) vs normalized tables vs "workflow as code". Write ADR-004
**Score:** __/28

## W6 - Data Layer + LLM Gateway v0 + First AI Use Case
**🎯 A6**
- [ ] JPA: optimistic locking on workflow publish; fix a deliberate N+1 (workflow → steps) 3 ways; keyset pagination on runs
- [ ] **orbit-llm-gateway v0 (Go)**: `POST /v1/chat` for 2 providers (one hosted + **Ollama** locally) behind a `Provider` interface (Strategy + Adapter); **SSE streaming passthrough**; timeouts; retries on 429/5xx with backoff; token usage in the response
- [ ] **UC1 v0**: classify a support ticket → **structured JSON** (category, priority, entities) validated against a schema; on invalid output, **re-ask with the validation error** (≤ 2 attempts)
- **Acceptance:** ≥ 85% accuracy on a 50-ticket labeled set you create; the gateway adds < 10 ms p99 overhead (measure against a mock provider)

**🔬 Lab:** 5M rows in `runs`; optimize 5 queries (composite, partial, covering indexes) with `EXPLAIN (ANALYZE, BUFFERS)` before and after ([[PostgreSQL Internals]])
**🧠 Cognitive:** *Predict → Verify*: predict the chosen plan and row estimates before each EXPLAIN
**🌀 Open:** Where do LLM request/response payloads (up to 200 KB) live? Postgres jsonb vs S3 (**claim check**) vs ClickHouse. Include cost math
**Score:** __/28

## W7 - Multi-Tenancy & Security
**🎯 A7**
- [ ] Keycloak (org per tenant), JWT resource server, roles OWNER/BUILDER/VIEWER, method security
- [ ] API keys: generate `orb_live_<prefix>_<secret>`, store a **hash**, look up by prefix, constant-time compare, rotate/revoke
- [ ] **Postgres Row-Level Security** keyed on `app.tenant_id` set per transaction; prove that forgetting a `WHERE` can't leak data
- [ ] **Idempotency-Key starter** (a custom Spring Boot starter, Redis-backed): same key + same body → the same response; same key + a different body → 422
- **Acceptance:** an automated cross-tenant attack suite (20 cases: IDOR/BOLA, key reuse, JWT tampering) → all blocked

**🔬 Lab:** PortSwigger: access control + JWT labs (≥ 6)
**🧠 Cognitive:** draw OAuth2 Auth Code + PKCE from memory, then check it against the RFC; list what each parameter defends against
**🌀 Open:** RLS vs app-level filters vs schema-per-tenant vs DB-per-tenant for 10 → 10,000 tenants
**Score:** __/28

## W8 - Tool Calling, gRPC & Quotas
**🎯 A8**
- [ ] **orbit-worker (Go)** with the **tool-calling loop from scratch**: model → `tool_use` → validate args against JSON Schema → execute → `tool_result` → model; max iterations, per-tool timeout, **tool-output truncation**, parallel tool calls
- [ ] Built-in tools: `http_request` (with an allowlist!), `sql_readonly` (read-only role + `statement_timeout` + row limit), `calculator`, `github_create_issue`
- [ ] **UC1 v1**: triage → if bug → create a GitHub issue via the tool → return a link
- [ ] gRPC contracts in `proto/` with **buf** (lint + breaking checks); a Java client ↔ Go server
- [ ] Gateway quotas: **token bucket per tenant in Redis Lua** (RPM + TPM); 429 + `Retry-After`
- **Acceptance:** 200 concurrent goroutines never over-admit (verified by counting); the tool loop terminates on a looping model (use a mock that always calls a tool)

**🔬 Lab:** mini Redis: add replication *or* RDB persistence; Wireshark a gRPC call ([[Network Stack Internals]])
**🧠 Cognitive:** *Pre-mortem*: 10 ways the tool-calling loop can fail in production (injection via tool output, a huge result, a hung tool, a non-idempotent retry…)
**🌀 Open:** Design the tool-definition schema + versioning. How do you evolve a tool without breaking published workflows?
**Score:** __/28

## W9 - Streaming, GraphQL, UI & the v1 Ship
**🎯 A9**
- [ ] **orbit-stream (Go)**: SSE endpoint fanning out tokens + run events from Redis pub/sub; `Last-Event-ID` resume (keep the last N events per run in a Redis stream)
- [ ] GraphQL (Spring for GraphQL): workflows → versions → runs → steps with `@BatchMapping`
- [ ] **UC2 v0**: chat playground with streaming + conversation memory (summarize after 10 turns)
- [ ] orbit-web: playground, run timeline, JSON workflow editor; `docker compose up` brings up everything
- [ ] GitHub Actions: Java + Go matrices, cached builds < 6 min

**⚫ Phase boss fight:** load test v1 with **200 concurrent streaming chats + 50 runs/s** against a mock provider (realistic TTFT/ITL distributions). Find and fix **2 bottlenecks** using JFR/async-profiler + pprof. Publish the blog post "Building an LLM gateway in Go"
**🧠 Cognitive:** *Self-review*: reread your W5 ADRs as a critical reviewer; write 3 critiques each
**Score:** __/28
