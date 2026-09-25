---
tags: [roadmap, phase]
weeks: W15–W18
dates: 2027-01-04 → 2027-01-31
---
# Phase 4: Cloud Native, Ops & Data (W15–W18)

> [!goal] Exit criteria
> - Deploy every Orbit service to Kubernetes with Helm: probes, resource requests/limits, HPA, ConfigMaps/Secrets, NetworkPolicies
> - Put Envoy / a gateway at the edge with rate limiting, JWT validation, and routing
> - Provision cloud infrastructure with Terraform (remote state, modules), then destroy it
> - Run a CI/CD pipeline: test → build → scan → push → GitOps deploy (ArgoCD)
> - Follow a single request across Java + Go services in one distributed trace
> - Define SLIs/SLOs, run a k6 load test, and write a short capacity report
> - Run a CDC pipeline: Postgres → Debezium → Kafka → ClickHouse
> - Write a Kubernetes operator and an Envoy ext_authz server in Go; sandbox untrusted code with gVisor
> - **Ship [[Orbit v3 - Cloud Native]]** · **Start applying in W15**


## 🔥 This phase's work
| Track | Where |
|---|---|
| 🎯 Weekly assignments, labs, cognitive tasks, open questions | [[Assignments - Phase 4]] (A15–A18) |
| ⚙️ Internals | [[Container Internals]] · [[Kubernetes Internals]] · [[Envoy Internals]] |
| 🧩 Design patterns | [[Distributed & Cloud Patterns]] (sidecar, operator, valet key, claim check, pipes & filters, cells) |
| ⚫ Boss fight | Production Day: cloud deploy + 1-hour soak + 3 injected failures, SLOs held, < $10 |
| 🧠 Daily/weekly drills | [[Cognitive Drills]] · self-grade with [[Grading Rubric]] |

## Tracks
[[Docker]] · [[Kubernetes]] · [[Envoy, Gateways & Service Mesh]] · [[Cloud (AWS)]] · [[Terraform & IaC]] · [[CI-CD & GitOps]] · [[Observability]] · [[SRE & Reliability]] · [[Security Engineering]] · [[Data Pipelines]]

## Reading
- *Kubernetes Up & Running* 3e · *Kubernetes the Hard Way* (Hightower), do it once
- *Terraform: Up & Running* 3e (Brikman)
- *Site Reliability Engineering* + *The SRE Workbook* (Google, free): SLO chapters
- *Observability Engineering* (Majors et al.)
- *Fundamentals of Data Engineering* (Reis & Housley): lifecycle chapters
- *Release It!* 2e (Nygard): stability patterns

## Cost guardrails ☁️
- [ ] Set up an AWS Budget alert ($10 and $25)
- [ ] Prefer local (kind/k3d, LocalStack) and destroy cloud resources after each session
- [ ] Never commit credentials; use `aws-vault` or SSO + short-lived creds

## Retro
- What stuck:
- What didn't:
- Skill Matrix delta:
