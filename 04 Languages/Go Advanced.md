---
tags: [language, go]
phase: 1
---
# 🐹 Go Advanced (target: Go 1.25+)

## 1. Language mastery
- [ ] Types, structs, embedding (composition), methods, pointer vs value receivers
- [ ] Interfaces: implicit satisfaction, small interfaces, "accept interfaces, return structs", nil-interface gotcha
- [ ] Slices (len/cap/backing array aliasing), maps, strings/runes/bytes
- [ ] Errors: wrapping (`%w`), `errors.Is/As`, sentinel vs typed errors, `panic`/`recover` (rarely)
- [ ] Generics: type parameters, constraints, when to use them (and when not)
- [ ] Iterators (`range` over functions, `iter.Seq`), `slices`/`maps` packages
- [ ] `defer` semantics, closures, and the loop variable (changed in 1.22)
- [ ] Packages, modules, internal packages, project layout (keep it simple)

## 2. Concurrency → [[Concurrency]]
- [ ] Goroutines, channels, select, `context`, `sync`, `errgroup`, `singleflight`
- [ ] Scheduler (G-M-P), preemption, `GOMAXPROCS` (container-aware by default in newer versions; verify for yours)
- [ ] Go memory model; race detector

## 3. Runtime & performance
- [ ] Escape analysis (`go build -gcflags=-m`), stack vs heap
- [ ] GC (concurrent mark-sweep, `GOGC`, `GOMEMLIMIT`)
- [ ] `pprof` (CPU, heap, goroutine, mutex, block), `go tool trace`, benchmarks + `benchstat`
- [ ] `sync.Pool`, preallocation, `strings.Builder`

## 4. Stdlib you must know
`net/http` (incl. the 1.22+ routing patterns), `encoding/json`, `database/sql`, `context`, `log/slog`, `testing`, `io`, `bufio`, `time`, `os/signal`

## 5. Testing
- [ ] Table-driven tests, subtests, `t.Parallel`, test helpers, golden files
- [ ] Fuzzing (`go test -fuzz`), benchmarks, `httptest`
- [ ] Mocks via interfaces (or `gomock`/`mockery`), Testcontainers-go

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 Tour of Go concurrency exercises; Go by Example end to end
- [ ] 🟡 Concurrent crawler: worker pool + rate limit + context cancel + `goleak`
- [ ] 🟡 *Writing an Interpreter in Go* ch. 1–3 → `orbit-expr`
- [ ] 🔴 Build your own Redis in Go (CodeCrafters/codingchallenges)
- [ ] 🔴 pprof a leaky, allocation-heavy service; cut allocations by 50%
- [ ] ⚫ **1BRC in Go** (W4) · MIT 6.5840 labs (Phase 3)

## 🧠 Cognitive tasks
- [ ] Predict → verify: escape analysis of 5 functions (`-gcflags=-m`)
- [ ] Reproduce the typed-nil-interface bug and slice aliasing; explain both from the runtime structs
- [ ] Trade-off debate: channels vs mutex for Orbit's lease table

## 🛰️ Orbit integration
- [ ] `orbit-dag` → orbit-engine; orbit-worker, llm-gateway, hooks, stream are all Go

> [!info] Go deeper
> ⚙️ [[Go Runtime Internals]] · 🧩 [[GoF Patterns (Java & Go)]] · [[Concurrency Patterns]]

## Resources
- *Learning Go* 2e (Bodner) ⭐ · *Concurrency in Go* (Cox-Buday) ⭐ · *100 Go Mistakes and How to Avoid Them* (Harsanyi) ⭐
- *Let's Go* / *Let's Go Further* (Edwards) → [[Go Backend Development]]
- Tour of Go, Go by Example, Effective Go, the Go blog, Ardan Labs *Ultimate Go* (Bill Kennedy)

## Interview questions #interview-q
- How does the Go scheduler work? What's the G-M-P model?
- What's a goroutine leak? How do you prevent one?
- Why can a nil pointer inside an interface make `err != nil` true?
- Buffered vs unbuffered channels: semantics and use cases
