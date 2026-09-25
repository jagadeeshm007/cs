---
tags: [language, python]
phase: 1
---
# 🐍 Python Essentials (goal: productive for scripting + AI)

You don't need Python mastery. You need enough to use the AI ecosystem (LangGraph, evals, notebooks), where Python is the first-class citizen.

## Checklist
- [ ] Syntax, comprehensions, dataclasses, type hints, f-strings
- [ ] Virtual envs + package management with **uv** (modern and fast); `pyproject.toml`
- [ ] `asyncio` basics (async/await, gather), since AI SDKs are async-heavy
- [ ] Pydantic (data validation), used everywhere in AI tooling
- [ ] FastAPI basics (to expose a Python agent as a service)
- [ ] Jupyter notebooks for experiments
- [ ] `requests`/`httpx`, `pytest`

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 A uv project + pytest + ruff
- [ ] 🟡 FastAPI service with Pydantic models + SSE streaming
- [ ] 🟡 asyncio: fan out 50 HTTP calls with a semaphore; compare with Go

## 🧠 Cognitive tasks
- [ ] Transfer: map Python async concepts to Go goroutines and Java virtual threads

## 🛰️ Orbit integration
- [ ] orbit-agents (LangGraph) and orbit-evals are Python services

> [!info] Go deeper
> 🧩 [[AI & Agent Patterns]]

## Resources
- Official Python tutorial · *Fluent Python* 2e (reference for later) · FastAPI docs
