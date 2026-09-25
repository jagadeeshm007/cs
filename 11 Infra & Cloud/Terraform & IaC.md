---
tags: [infra, terraform, iac]
phase: 4
---
# 🏗️ Terraform & Infrastructure as Code

- [ ] Why IaC: reproducibility, review, drift detection
- [ ] HCL: providers, resources, data sources, variables, outputs, locals
- [ ] **State**: remote backend (S3 with native state locking), state locking, `import`, `moved` blocks
- [ ] Modules: composition, versioning, the public registry
- [ ] Environments: workspaces vs directory-per-env; Terragrunt (awareness)
- [ ] Plan/apply in CI with review; policy as code (OPA/Conftest, Checkov/tfsec)
- [ ] **OpenTofu** (the open-source fork): know it exists
- [ ] Alternatives: Pulumi (IaC in Go/Java/TS), AWS CDK, Crossplane (K8s-native)

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟡 Modules for network, cluster, database, and bucket; remote state
- [ ] 🔴 `plan` on PR / `apply` on merge with approval; Checkov/tfsec policy checks
- [ ] ⚫ Import an existing resource, refactor it with `moved` blocks, zero diff

## 🧠 Cognitive tasks
- [ ] Pre-mortem: 5 ways Terraform can destroy production, and the guardrails for each

## 🛰️ Orbit integration
- [ ] The Orbit cloud environment

> [!info] Go deeper
> ⚙️ [[Kubernetes Internals]]

## Resources
- *Terraform: Up & Running* 3e (Brikman) ⭐ · HashiCorp tutorials
