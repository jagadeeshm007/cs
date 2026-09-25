---
tags: [assignments, phase-4]
weeks: W15–W18
---
# 📝 Assignments: Phase 4 (Cloud Native, Ops, Data)

## W15 - Kubernetes-Native Orbit + an Operator 🔴
**🎯 A15**
- [ ] Helm charts for all services; readiness vs liveness done right; `preStop` + graceful shutdown; PDBs; resource requests/limits from measured usage
- [ ] Workers: on SIGTERM → stop claiming → finish or **release leases** → exit
- [ ] **KEDA** ScaledObject on queue depth (Postgres/Prometheus scaler) or Kafka lag
- [ ] **kubebuilder operator**: an `OrbitWorkerPool` CRD (tier, minReplicas, maxReplicas, stepTypes) → reconciles a Deployment + ScaledObject + NetworkPolicy; status conditions; owner references
- **Acceptance:** a rolling deploy under load → 0 failed runs, 0 5xx; delete the Deployment → the operator recreates it

**🔬 Lab:** Kubernetes the Hard Way (or at least bootstrap etcd + the API server by hand) ([[Kubernetes Internals]])
**🧠 Cognitive:** trace `kubectl apply` through every component in writing, then verify it with events/audit logs
**🌀 Open:** Should enterprise tenants get dedicated worker pools/namespaces? Compare cells vs shared pools
**Score:** __/28

## W16 - Edge, Sandbox & IaC
**🎯 A16**
- [ ] **Envoy Gateway** (Gateway API): HTTPRoutes/GRPCRoutes, JWT authn (Keycloak JWKS), global rate limit, **SSE-safe timeouts**
- [ ] **ext_authz server in Go** validating Orbit API keys (with a cache + revocation via Redis pub/sub)
- [ ] **Code sandbox** for the `code` step: gVisor RuntimeClass (`runsc`), no network, read-only rootfs, CPU/mem/pids limits, a 10 s timeout, output size caps
- [ ] **Terraform**: VPC + k3s-on-EC2 (or EKS) + RDS + S3 + IAM (least privilege); remote state; `terraform destroy` verified
- **Acceptance:** 10 malicious code snippets (fork bomb, network exfiltration, reading host files, infinite loop, memory bomb) → all contained

**🔬 Lab:** **Containers from scratch in Go** ([[Container Internals]])
**🧠 Cognitive:** *Predict*: which proxy/timeouts will break a 5-minute LLM stream? Verify each one
**🌀 Open:** Sandboxing untrusted LLM-generated code: gVisor vs Firecracker vs WASM (wazero) vs a remote sandbox service
**Score:** __/28

## W17 - Observability & Delivery
**🎯 A17**
- [ ] OpenTelemetry in Java (agent), Go (SDK), and Python; **GenAI semantic conventions** (model, input/output tokens, cost) on spans; trace context through **Kafka headers**
- [ ] Collector with **tail sampling** (keep errors + slow + 5% of the rest)
- [ ] Grafana: RED per service, queue wait, TTFT/ITL, tokens and **$ per tenant**
- [ ] SLOs + multi-window **burn-rate alerts**; 3 runbooks
- [ ] GitHub Actions → build → test → Trivy/Semgrep/govulncheck → cosign → GHCR → **ArgoCD**; **Argo Rollouts canary** for llm-gateway gated on Prometheus analysis
- **Acceptance:** a deliberately bad gateway release is auto-rolled back by the canary analysis

**🔬 Lab (🔴):** a **mini tracer in Go**: spans, W3C `traceparent` injection/extraction over HTTP and Kafka headers, export to a JSON file, then render a waterfall
**🧠 Cognitive:** *Symptom → hypotheses*: 3 prompts from [[Cognitive Drills]], answered using only your dashboards
**🌀 Open:** SLOs for an LLM platform when the providers themselves only offer ~99.5%: what can you promise?
**Score:** __/28

## W18 - Ingestion Pipeline, Analytics & Production Day
**🎯 A18**
- [ ] **Ingestion (pipes & filters)**: presigned S3 upload (**valet key**) → event → parse (PDF/HTML/Markdown) → chunk → embed in batches (rate-limited, retried) → pgvector upsert; **idempotent + resumable** (content hashes)
- [ ] Usage events + CDC → **ClickHouse**; materialized views for tokens/cost per tenant per hour; Grafana dashboards
- [ ] STRIDE threat model; NetworkPolicies default-deny; External Secrets
- **Acceptance:** kill the pipeline mid-way through 1,000 docs → resume → no duplicate chunks; ClickHouse totals match Postgres totals

**🔬 Lab:** a Kafka Streams or Flink SQL job: tokens per tenant per 1-min tumbling window with late-event handling

**⚫ Phase boss fight: Production Day.** Terraform up the cloud env → ArgoCD deploy → 1-hour k6 soak (UC1 + UC2 + UC3 mix) → inject 3 failures (node drain, provider outage, DB failover) → hold the SLOs → `terraform destroy`. **Budget: < $10.** Write the report with graphs
**🧠 Cognitive:** *Fermi*: estimate the monthly infra + LLM cost for 1,000 tenants at 50 runs/day each, then check it against your ClickHouse data
**Score:** __/28
