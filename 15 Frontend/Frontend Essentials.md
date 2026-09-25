---
tags: [frontend, react, typescript]
phase: 2
---
# 🎨 Frontend Essentials (enough to ship end to end)

Goal: build Orbit's UI yourself (workflow builder, playground, run viewer) and understand the frontend constraints that affect backend/API design. This is not frontend mastery.

## Checklist
- [ ] HTML semantics, CSS flexbox/grid, responsive basics, **Tailwind CSS**
- [ ] JavaScript essentials: async/await, fetch, modules, closures, event loop
- [ ] **TypeScript**: types, interfaces, generics, unions/narrowing
- [ ] **React**: components, props/state, hooks (`useState`, `useEffect`, `useMemo`), lists/keys, forms
- [ ] Data fetching: **TanStack Query** (caching, retries, invalidation)
- [ ] Routing (React Router) or **Next.js** (App Router, server components: awareness)
- [ ] Auth in the browser: OIDC with PKCE (Keycloak JS / oidc-client-ts), token storage trade-offs
- [ ] Realtime: SSE token streaming, live run timeline
- [ ] **React Flow** for the visual workflow builder
- [ ] Component library: shadcn/ui
- [ ] Web performance basics: Core Web Vitals, bundle size, lazy loading
- [ ] Tooling: Vite, ESLint, Prettier

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 A TS + React + Vite + Tailwind + TanStack Query starter
- [ ] 🟡 A playground chat with SSE token streaming
- [ ] 🔴 A **workflow builder** with React Flow (DAG editing → JSON definition)
- [ ] ⚫ A run timeline / trace viewer (step waterfall with tokens and cost)

## 🧠 Cognitive tasks
- [ ] Predict which API shapes make the UI simple; adjust GraphQL accordingly

## 🛰️ Orbit integration
- [ ] orbit-web: builder, playground, runs, approvals inbox, knowledge UI

> [!info] Go deeper
> 🧩 [[GoF Patterns (Java & Go)]] (Observer, Composite)

## Resources
- react.dev ⭐ · TypeScript Handbook · TanStack Query docs · *Learning TypeScript* (Goldberg)
