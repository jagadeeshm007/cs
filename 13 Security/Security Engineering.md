---
tags: [security]
phase: 2-4
---
# 🔒 Security Engineering (for backend engineers)

## AppSec
- [ ] **OWASP Top 10** (web) and **OWASP API Security Top 10** ⭐: injection, broken auth, BOLA/IDOR, SSRF, mass assignment
- [ ] **OWASP Top 10 for LLM Applications**: prompt injection, insecure output handling, excessive agency ⭐
- [ ] Input validation, output encoding, parameterized queries
- [ ] AuthN/AuthZ → [[Spring Security]]: OAuth2/OIDC, JWT pitfalls (`alg=none`, no expiry, secrets in the payload)
- [ ] Authorization models: RBAC, ABAC, **ReBAC (Google Zanzibar → OpenFGA/SpiceDB)**; policy engines (OPA)
- [ ] Session security, CSRF, CORS, security headers (CSP, HSTS)
- [ ] Rate limiting & abuse prevention (bots in flash sales!)

## Crypto basics (conceptual)
- [ ] Hashing vs encryption vs encoding; salted password hashing (argon2/bcrypt)
- [ ] Symmetric (AES-GCM) vs asymmetric (RSA/ECDSA); signatures; HMAC
- [ ] TLS/mTLS, certificates, PKI; envelope encryption with KMS
- [ ] Post-quantum crypto (awareness: hybrid key exchange is being rolled out in TLS)

## Infra & supply chain
- [ ] Secrets management (Vault, AWS Secrets Manager, External Secrets); **never in git**
- [ ] Least-privilege IAM; K8s RBAC; NetworkPolicies; Pod Security
- [ ] Dependency scanning (Dependabot, OWASP dependency-check, `govulncheck`), SAST (Semgrep, CodeQL), image scanning (Trivy)
- [ ] SBOM, signing (Sigstore/cosign), SLSA
- [ ] Zero-trust networking; mTLS via a mesh

## Data & privacy
- [ ] PII handling, encryption at rest/in transit, data retention; GDPR and India's DPDP Act (awareness)
- [ ] Audit logging
- [ ] Payments: PCI-DSS awareness (use tokenized providers)

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 PortSwigger labs: access control, JWT, SSRF, SQLi
- [ ] 🟡 A cross-tenant attack suite against Orbit (BOLA/IDOR, key reuse, JWT tampering)
- [ ] 🔴 SSRF protection for the `http_request` tool (allowlists, block private IP ranges, DNS rebinding)
- [ ] 🔴 A sandbox escape test suite for the `code` step
- [ ] ⚫ **Red-Team Day** (W22): prompt injection, exfiltration, excessive agency

## 🧠 Cognitive tasks
- [ ] STRIDE threat model per Orbit version
- [ ] Transfer: map classic AppSec controls to agent/tool security

## 🛰️ Orbit integration
- [ ] Security gates in CI; tenant isolation; the tool permission model

> [!info] Go deeper
> 🧩 [[Anti-Patterns & Code Smells]] · 🤖 [[Evals, Guardrails & LLMOps]]

## Resources
- OWASP cheat sheets ⭐ · *API Security in Action* (Madden) · PortSwigger Academy · *Security Engineering* (Anderson, reference)
