---
tags: [ai, mcp, protocols]
phase: 5
---
# 🔌 MCP (Model Context Protocol)

> An open protocol that standardizes how AI applications (hosts/clients) connect to external **tools, resources, and prompts** through MCP servers. "USB-C for AI integrations."

## Concepts
- [ ] Architecture: host → client → server; JSON-RPC 2.0 messages; capability negotiation
- [ ] Transports: **stdio** (local) and **Streamable HTTP** (remote)
- [ ] Server primitives: **tools** (model-controlled actions), **resources** (app-controlled context), **prompts** (user-controlled templates)
- [ ] Client features: sampling, roots, elicitation
- [ ] Auth for remote servers: OAuth 2.1-based authorization
- [ ] Security: tool poisoning, prompt injection via tool output, confused deputy, least privilege, user consent for sensitive tools ⭐
- [ ] Ecosystem: official SDKs (TypeScript, Python, **Java**, **Go**, Kotlin, C#), MCP Inspector, registries

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 Run an existing MCP server (filesystem/GitHub) with MCP Inspector
- [ ] 🟡 **Orbit MCP server** in Spring AI (tools + resources)
- [ ] 🔴 A read-only Go MCP server (official Go SDK) for run logs/metrics
- [ ] 🔴 Remote HTTP transport with OAuth + per-tool approval
- [ ] ⚫ An MCP client in orbit-tools: dynamic tool discovery from external servers with scopes

## 🧠 Cognitive tasks
- [ ] Threat model: tool poisoning, a confused deputy, injection via tool output

## 🛰️ Orbit integration
- [ ] Orbit is usable from Claude Desktop / Claude Code / IDEs as an MCP server

> [!info] Go deeper
> 🧩 [[AI & Agent Patterns]] · 🔒 [[Security Engineering]]

## Resources
- modelcontextprotocol.io (spec, docs, quickstarts) ⭐ · SDK repos on GitHub · Spring AI MCP docs
