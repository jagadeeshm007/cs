---
tags: [go, microservices, tooling]
phase: 3
---
# 🔧 Go Microservices & Tooling

- [ ] Makefile / Taskfile; `golangci-lint`; `govulncheck`; `go generate`
- [ ] Multi-stage Docker builds → distroless/scratch images (~15 MB)
- [ ] gRPC interceptors: auth, logging, tracing, retries; deadlines propagation
- [ ] Kafka consumer group patterns with franz-go; batch processing; manual commits after processing
- [ ] Circuit breaker (sony/gobreaker), retries with backoff (cenkalti/backoff), `singleflight`, rate limiting (`x/time/rate`)
- [ ] Feature flags (OpenFeature Go SDK)
- [ ] Temporal Go SDK (durable workflows) ⭐
- [ ] Writing a Kubernetes operator/controller with **kubebuilder** (advanced; very valued in platform teams)
- [ ] CLI tools with cobra (many infra tools are Go CLIs)

## Why Go matters in 2026
Kubernetes, Docker, etcd, Prometheus, Terraform, Envoy's control planes, and most cloud-native tooling are written in Go. Being strong in Go opens platform/infra/SRE roles as well as backend ones.

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟡 gRPC interceptors: auth, logging, tracing, deadline propagation
- [ ] 🔴 franz-go consumer with manual commits after processing + batching
- [ ] 🔴 **kubebuilder operator** `OrbitWorkerPool` (W15)
- [ ] ⚫ An Envoy **ext_authz** gRPC server (W16); a go-control-plane xDS server (open)

## 🧠 Cognitive tasks
- [ ] Code archaeology: read `net/http/server.go` `Serve` + `conn.serve`

## 🛰️ Orbit integration
- [ ] Every Go service's build, lint, and vuln scan in CI

> [!info] Go deeper
> ⚙️ [[Go Runtime Internals]] · [[Kubernetes Internals]]

