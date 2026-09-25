---
tags: [patterns, gof, java, go]
---
# 🏛️ GoF Patterns: Java vs Go, in the wild, in Orbit

> [!tip] Language lens
> Java expresses patterns with **classes + interfaces + inheritance + frameworks**. Go expresses the same ideas with **small interfaces, first-class functions, embedding, and closures**. Many GoF patterns collapse into "pass a function" in Go.

## Creational
| Pattern | Intent | Java / in the wild | Go idiom | Orbit usage |
|---|---|---|---|---|
| **Factory Method** | Defer instantiation to a creator | `BeanFactory`, `Calendar.getInstance()` | `NewX(...)` constructors returning interfaces | `StepExecutorFactory.forType("llm")` |
| **Abstract Factory** | Families of related objects | JDBC `Connection` → `Statement` | Interface returning a family of interfaces | Provider SDK family: client + tokenizer + embedder |
| **Builder** | Step-by-step complex construction | `RestClient.builder()`, Lombok `@Builder`, records + builders | ⭐ **Functional options**: `NewServer(addr, WithTimeout(5*time.Second))` | `WorkflowDefinition.builder()`, gateway client options |
| **Singleton** | One instance | Spring singleton scope, enum singleton | `sync.Once`, a package-level var | Config, provider registry (prefer DI over global singletons) |
| **Prototype** | Clone existing objects | `clone()`, prototype scope | Struct copy (watch slice/map aliasing!) | Clone a workflow version to create a draft |

## Structural
| Pattern | Intent | Java / in the wild | Go idiom | Orbit usage |
|---|---|---|---|---|
| **Adapter** | Convert one interface to another | `HandlerAdapter`, `Arrays.asList` | `http.HandlerFunc` adapts a func to `http.Handler` ⭐ | Anthropic/OpenAI/Ollama responses → a common `ChatResponse` |
| **Decorator** | Add behavior by wrapping | `java.io` streams, `Collections.synchronizedList` | ⭐ **Middleware**: `func(http.Handler) http.Handler` | Gateway: logging → auth → quota → cache → provider |
| **Proxy** | Control access to an object | **Spring AOP**, JPA lazy proxies | `httputil.ReverseProxy`, gRPC interceptors | Tool proxy that enforces scopes + approvals |
| **Facade** | A simple API over a complex subsystem | `JdbcTemplate`, `RestTemplate` | Package-level API over internal packages | `OrbitClient` SDK |
| **Composite** | Tree of uniform objects | UI trees, `CompositeCacheManager` | `io.MultiWriter`, an interface on tree nodes | Workflow DAG: `parallel`/`map` steps containing steps |
| **Bridge** | Separate abstraction from implementation | JDBC API ↔ drivers, SLF4J ↔ Logback | `slog.Logger` ↔ `slog.Handler` ⭐ | Vector store abstraction ↔ pgvector/Qdrant |
| **Flyweight** | Share fine-grained immutable state | `Integer.valueOf` cache, String pool | Interned strings, shared read-only structs | Shared tokenizer vocab, prompt templates |

## Behavioral
| Pattern | Intent | Java / in the wild | Go idiom | Orbit usage |
|---|---|---|---|---|
| **Strategy** ⭐ | Swap algorithms | `Comparator`, `PlatformTransactionManager` | An interface or a `func` type | Retry policies, routing policies, chunking strategies |
| **Chain of Responsibility** | Pass along handlers | Servlet filters, Security `FilterChain` | Middleware chains, gRPC interceptors | Guardrail chain: PII → injection check → schema |
| **Command** | Request as an object (queue, retry, undo) | `Runnable`, `Callable` | Structs with `Execute(ctx)`, closures | **Each step execution is a command** in the task queue |
| **State** ⭐ | Behavior depends on state | Order lifecycles, Spring Statemachine | A state enum + transition table, or state funcs (Rob Pike's lexer) | Run/step lifecycle: PENDING → RUNNING → WAITING → COMPLETED/FAILED/COMPENSATING |
| **Observer** | Notify subscribers | `ApplicationEventPublisher`, listeners | Channels, callbacks | Run events → stream service, webhooks |
| **Template Method** | Skeleton with overridable steps | `JdbcTemplate`, `AbstractController` | Rare → compose with function params | Base step executor: validate → execute → record |
| **Iterator** | Sequential access | `Iterator`, Streams | `iter.Seq`, range-over-func | Paginated run history cursor |
| **Mediator** | Centralize communication | Message brokers, `ApplicationEventMulticaster` | A central goroutine owning state | Supervisor agent coordinating sub-agents |
| **Memento** | Capture and restore state | Undo stacks | Snapshots | **Run checkpoints**, LangGraph checkpoints |
| **Interpreter** | Evaluate a language | SpEL, regex | ⭐ Pratt parser (*Writing an Interpreter in Go*) | `orbit-expr` conditions |
| **Visitor** | Operations over a structure | `FileVisitor`, compiler ASTs | Type switch over a sealed-ish interface | Validate/optimize/render a workflow DAG; **modern Java: sealed interfaces + pattern-matching `switch`** |

## SOLID (quick reference)
**S**ingle responsibility · **O**pen/closed (extend via Strategy/Decorator) · **L**iskov substitution · **I**nterface segregation (Go's small interfaces!) · **D**ependency inversion (depend on ports; adapters at the edges)

## 🔬 Katas
- [ ] Implement the LLM provider layer: Strategy + Adapter + Decorator (retry, logging, cache) in **both** languages
- [ ] The step lifecycle as a State pattern with an explicit transition table + property tests (no illegal transitions)
- [ ] Visitor in classic Java vs sealed interfaces + `switch` pattern matching → compare the readability
- [ ] Go functional options vs a Java builder for the same `GatewayClient` config
- [ ] Refactor a 200-line `if/else` step runner into Command + Factory + Strategy
