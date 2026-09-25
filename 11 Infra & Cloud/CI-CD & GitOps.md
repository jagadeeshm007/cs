---
tags: [infra, cicd, gitops]
phase: 4
---
# 🔁 CI/CD & GitOps

## Checklist
- [ ] Git mastery: branching (trunk-based ⭐), rebase vs merge, interactive rebase, bisect, conventional commits
- [ ] **GitHub Actions**: workflows, jobs, matrices, caching (Maven/Gradle/Go), reusable workflows, OIDC to AWS (no static keys ⭐)
- [ ] Pipeline stages: lint → unit test → integration test (Testcontainers) → build → SAST/dependency scan → image build → sign → push → deploy
- [ ] **GitOps with ArgoCD** (or Flux): app-of-apps, sync policies, drift detection
- [ ] Progressive delivery: Argo Rollouts canary with metric analysis
- [ ] Monorepo vs polyrepo; affected-only builds
- [ ] Release management: semantic versioning, changelogs, release-please
- [ ] Supply chain security: SBOM, cosign signing, SLSA levels, Dependabot/Renovate
- [ ] DORA metrics: deploy frequency, lead time, change failure rate, time to restore

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟡 A monorepo CI with path filters, Java + Go matrices, and caches (< 6 min)
- [ ] 🔴 OIDC to AWS (no static keys); cosign signing; SBOMs
- [ ] 🔴 ArgoCD app-of-apps; Argo Rollouts canary with Prometheus analysis
- [ ] ⚫ An **eval gate**: PRs touching prompts/models must pass orbit-evals

## 🧠 Cognitive tasks
- [ ] Measure your own DORA metrics weekly

## 🛰️ Orbit integration
- [ ] Every Orbit service ships through this pipeline

> [!info] Go deeper
> 🧩 [[Distributed & Cloud Patterns]] (canary, feature flags)

## Resources
- GitHub Actions docs · argo-cd.readthedocs.io · *Accelerate* (Forsgren, Humble, Kim) ⭐ · *Continuous Delivery* (Humble & Farley)
