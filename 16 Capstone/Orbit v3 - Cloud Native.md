---
tags: [capstone, orbit]
version: v3
weeks: W15–W18
---
# Orbit v3: Cloud Native, Observable & Data-Driven (Phase 4)

## Scope
- [ ] Images: Java < 150 MB (layered/Jib), Go < 20 MB (distroless/static); SBOM + cosign signatures; Trivy gate
- [ ] **Helm** charts; kind/k3d locally; probes with correct drain semantics; PDBs; HPA (api, gateway); **KEDA** autoscaling workers on queue depth / Kafka lag
- [ ] **Graceful worker shutdown**: on SIGTERM, stop claiming, finish or release leases
- [ ] **kubebuilder operator**: `OrbitWorkerPool` CRD → reconciles Deployment + KEDA ScaledObject + NetworkPolicy per tenant tier
- [ ] **Envoy Gateway** (Gateway API): routes, JWT authn (Keycloak JWKS), **ext_authz in Go** for API keys, global rate limit; SSE-safe timeouts/buffering
- [ ] **Code-execution sandbox** for the `code` step: gVisor (`runsc`) RuntimeClass, no network, CPU/memory/pids limits, read-only rootfs, timeouts
- [ ] **Terraform**: VPC + k3s/EKS + RDS Postgres + S3; remote state; destroy after sessions
- [ ] **CI/CD**: GitHub Actions → GHCR → **ArgoCD**; Argo Rollouts canary for llm-gateway gated on error rate + latency
- [ ] **OpenTelemetry** in Java, Go, and Python with **GenAI semantic conventions** (model, tokens, cost on spans); Collector tail sampling; Tempo/Prometheus/Loki/Grafana
- [ ] **SLOs**: run success rate, TTFT p95, queue wait p95; burn-rate alerts; runbooks
- [ ] **Ingestion pipeline** (pipes & filters): presigned S3 upload → event → parse → chunk → embed (batched, rate-limited) → pgvector upsert; idempotent + resumable
- [ ] **Analytics**: CDC + usage events → ClickHouse → Grafana cost/usage dashboards per tenant
- [ ] Security: STRIDE threat model, NetworkPolicies, External Secrets, Semgrep/govulncheck/Trivy in CI

## Definition of done
- [ ] 1-hour soak test in the cloud with 3 injected failures, SLOs held, **total cloud cost < $10**
- [ ] One trace spanning web → gateway → api → engine → Kafka → worker → llm-gateway → provider
- [ ] Blog: "Autoscaling AI workers on Kubernetes with KEDA and graceful lease handoff"
