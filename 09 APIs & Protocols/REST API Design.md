---
tags: [api, rest]
phase: 2
---
# 🔌 REST API Design

## Checklist
- [ ] Resource modeling (nouns), HTTP method semantics, **safe vs idempotent** methods
- [ ] Status codes used precisely (200/201/202/204, 400/401/403/404/409/412/422/429, 500/502/503/504)
- [ ] Errors: **RFC 9457 Problem Details** (`application/problem+json`)
- [ ] Pagination: offset vs **cursor/keyset**; filtering, sorting, sparse fieldsets
- [ ] Versioning strategies (URL, header, media type) and **backward-compatible evolution**
- [ ] **Idempotency keys** for POST (payments, bookings) ⭐
- [ ] Concurrency control: `ETag` + `If-Match` (optimistic), 412 Precondition Failed
- [ ] Caching: `Cache-Control`, `ETag`, `Last-Modified`, conditional GETs
- [ ] Long-running operations: 202 Accepted + status resource / webhooks
- [ ] Rate limiting headers (`RateLimit-*`, `Retry-After`)
- [ ] Webhooks: signing (HMAC), retries, idempotency
- [ ] **OpenAPI 3.1**: design-first vs code-first; codegen; springdoc
- [ ] HATEOAS: know what it is (rarely used in practice)

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟡 Design Orbit's public REST API design-first in OpenAPI 3.1: runs, workflows, approvals, API keys
- [ ] 🔴 Idempotency keys on `POST /runs` (same key + same body → the same run)
- [ ] 🔴 Long-running ops: `202 Accepted` + `Location` + status polling + webhooks
- [ ] ⚫ An SDK generated from OpenAPI in Go and TypeScript

## 🧠 Cognitive tasks
- [ ] Reverse engineering: study Stripe's and OpenAI/Anthropic's APIs; what idempotency, pagination, and error choices did they make?

## 🛰️ Orbit integration
- [ ] The public API of orbit-api + webhook contracts from orbit-hooks

> [!info] Go deeper
> 🧩 [[Enterprise & DDD Patterns]]

## Resources
- Microsoft REST API Guidelines · Google AIP (aip.dev) ⭐ · Zalando RESTful API Guidelines
- Stripe API docs (the gold standard for idempotency, errors, pagination)
