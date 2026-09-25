---
tags: [system-design, lld, java]
---
# 🔧 Low-Level Design & Machine Coding

Many companies (Flipkart, Swiggy, Uber, Atlassian, PhonePe, Razorpay, Amazon) have an **LLD / machine coding round**: 60–120 min to build working, extensible, tested code.

## Foundations
- [ ] OOP: encapsulation, abstraction, polymorphism, composition over inheritance
- [ ] **SOLID**, DRY, KISS, YAGNI, Law of Demeter
- [ ] UML class and sequence diagrams (just enough)
- [ ] Design patterns you actually use:
  - Creational: Factory, Abstract Factory, Builder, Singleton (and its problems)
  - Structural: Adapter, Decorator, Facade, Proxy, Composite
  - Behavioral: Strategy, Observer, State, Command, Chain of Responsibility, Template Method, Iterator
- [ ] Concurrency in LLD: thread-safe classes, locks per entity

## Machine-coding checklist (per round)
1. Clarify requirements (write them down), agree on scope
2. Identify entities → relationships → class diagram (5 min)
3. Define interfaces first (strategies, repositories)
4. Implement the core flow end to end → then extensions
5. In-memory storage behind a repository interface
6. Handle edge cases + concurrency
7. Write a driver/main + a few unit tests
8. Explain the extensibility points

## Problem list
- [ ] Parking lot · [ ] Splitwise · [ ] Snake & Ladder · [ ] Elevator system · [ ] Tic-tac-toe / chess
- [ ] LRU / LFU cache · [ ] Rate limiter · [ ] In-memory KV store with transactions · [ ] Logger framework
- [ ] Pub-sub / message queue · [ ] Task scheduler · [ ] Vending machine (State pattern)
- [ ] **BookMyShow** · [ ] Library management · [ ] ATM · [ ] Hotel booking · [ ] Cab booking
- [ ] Inventory management · [ ] Payment wallet · [ ] Notification service · [ ] Cricbuzz/scoreboard
- [ ] File system (Composite) · [ ] Meeting room scheduler · [ ] Distributed ID generator

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟡 2 timed machine-coding rounds per week in Phases 1–2, then 1 per week
- [ ] 🔴 **Orbit LLD set**: workflow engine (State + Command + Strategy), LLM gateway middleware (Decorator + Chain), tool registry (Registry + Adapter), rate limiter (Strategy), prompt template engine (Interpreter)
- [ ] ⚫ Implement one LLD problem in both Java and Go; compare the designs

## 🧠 Cognitive tasks
- [ ] Self-review after 7 days: find 3 smells in your own LLD solution
- [ ] Extensibility test: add a new requirement to a finished solution in 15 min; did your design survive?

## 🛰️ Orbit integration
- [ ] Class models for `Workflow`, `Step`, `Run`, `StepExecutor`, `RetryPolicy`, `StepState`

> [!info] Go deeper
> 🧩 [[GoF Patterns (Java & Go)]] · [[Anti-Patterns & Code Smells]]

## Resources
- *Head First Design Patterns* 2e ⭐ · refactoring.guru (patterns + refactoring, free) ⭐
- *Refactoring* 2e (Fowler) · *Clean Code* (take it with a grain of salt) · *A Philosophy of Software Design* ⭐
- GitHub "awesome-low-level-design" · workat.tech machine coding problems
