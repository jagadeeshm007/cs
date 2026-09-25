---
tags: [api, graphql]
phase: 2
---
# 🕸️ GraphQL

## Checklist
- [ ] Schema-first design: types, queries, mutations, subscriptions, input types, enums, interfaces/unions
- [ ] Resolvers and the execution model
- [ ] **N+1 problem → DataLoader** (batching + caching per request) ⭐
- [ ] Pagination (Relay connection spec / cursors)
- [ ] Errors (partial results), nullability design
- [ ] Security: query depth/complexity limits, persisted queries, authz in resolvers (field level)
- [ ] Caching challenges (POST, no HTTP cache) and solutions (persisted queries + GET, client caches)
- [ ] Federation (Apollo Federation / GraphQL Fusion) for microservices: awareness
- [ ] When NOT to use GraphQL

## Implementations
- Java: **Spring for GraphQL** (`@SchemaMapping`, `@BatchMapping`)
- Go: **gqlgen**

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟡 Spring for GraphQL: workflows → versions → runs → steps with `@BatchMapping`
- [ ] 🔴 Query depth/complexity limits + persisted queries
- [ ] ⚫ Subscriptions for run status vs SSE; compare them

## 🧠 Cognitive tasks
- [ ] Predict the number of SQL queries for a nested query with and without DataLoader

## 🛰️ Orbit integration
- [ ] The orbit-web UI data layer

> [!info] Go deeper
> 🧩 [[Enterprise & DDD Patterns]]

## Resources
- graphql.org/learn · *Production Ready GraphQL* (Giroux) · Spring for GraphQL docs
