---
tags: [go, backend]
phase: 2
---
# 🐹 Go Backend Development

> [!tip] Go philosophy
> Prefer the **stdlib + small libraries** over big frameworks. Explicit over magic. This is the opposite mindset from Spring, and knowing both makes you a stronger engineer.

## Stack choices (learn the default well; know the alternatives)
| Concern | Default | Alternatives |
|---|---|---|
| HTTP routing | `net/http` (1.22+ patterns) or **chi** | gin, echo, fiber |
| DB driver | **pgx** | `database/sql` |
| Queries | **sqlc** (SQL → type-safe Go) | GORM (know it, but avoid in hot paths), sqlx, ent, bun |
| Migrations | **goose** or golang-migrate / atlas | |
| Config | env + `caarlos0/env` or koanf | viper |
| Logging | **`log/slog`** | zap, zerolog |
| Validation | go-playground/validator | |
| gRPC | grpc-go + **buf** / **connect-go** | |
| GraphQL | **gqlgen** | |
| Kafka | **franz-go** | confluent-kafka-go, segmentio/kafka-go |
| Redis | go-redis | rueidis |
| Testing | stdlib + testify + testcontainers-go | |
| Observability | OpenTelemetry Go SDK + Prometheus client | |
| DI | manual constructor wiring | wire, fx |

## Checklist
- [ ] Project structure: `cmd/`, `internal/` (by domain), not "Java-style" layered packages
- [ ] Handler → service → repository with interfaces at the consumer side
- [ ] Middleware: logging, recovery, request ID, auth (JWT validation via JWKS), CORS, rate limiting
- [ ] Graceful shutdown (`signal.NotifyContext`, `server.Shutdown`)
- [ ] Timeouts everywhere (`http.Server` Read/Write/Idle timeouts, `context.WithTimeout` for DB/HTTP calls)
- [ ] Transactions with pgx; optimistic locking; `SELECT … FOR UPDATE SKIP LOCKED` job queues
- [ ] Errors → HTTP status mapping; problem+json
- [ ] Health/readiness endpoints; Prometheus metrics; pprof endpoint (protected)
- [ ] Integration tests with testcontainers-go

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 chi + pgx + sqlc + slog service with graceful shutdown
- [ ] 🟡 Middleware chain: request ID, logging, recovery, auth, rate limit (Decorator)
- [ ] 🔴 **orbit-llm-gateway**: provider adapters, SSE streaming passthrough, Lua quotas, fallback
- [ ] 🔴 A `SKIP LOCKED` job queue with leases + heartbeats
- [ ] ⚫ k6 + pprof: find and remove the top hotspot; show before/after flame graphs

## 🧠 Cognitive tasks
- [ ] Predict → verify: gateway overhead at p99 with 500 concurrent streams
- [ ] Trade-off debate: sqlc vs GORM for the engine's hot paths

## 🛰️ Orbit integration
- [ ] orbit-engine, orbit-worker, orbit-llm-gateway, orbit-hooks, and orbit-stream

> [!info] Go deeper
> ⚙️ [[Go Runtime Internals]] · [[Network Stack Internals]] · 🧩 [[Concurrency Patterns]]

## Resources
- *Let's Go* + *Let's Go Further* (Alex Edwards) ⭐ · *100 Go Mistakes* ⭐
- sqlc.dev, pgx docs, buf.build docs, connectrpc.com
- Ardan Labs *Service* repo (production service structure)
