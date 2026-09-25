---
tags: [java, spring, security]
phase: 2
---
# 🔐 Spring Security

## Core → Advanced
- [ ] Architecture: `SecurityFilterChain`, `DelegatingFilterProxy`, filter order, `SecurityContext`
- [ ] Authentication vs authorization; `AuthenticationManager`, providers, `UserDetailsService`
- [ ] Password hashing (bcrypt/argon2), `PasswordEncoder`
- [ ] Sessions vs stateless JWT; CSRF (when it matters), CORS
- [ ] Method security: `@PreAuthorize`, custom permission evaluators
- [ ] **OAuth2 / OIDC**: roles (resource owner, client, authorization server, resource server)
  - [ ] Authorization Code + **PKCE** flow · client credentials (service-to-service) · refresh tokens
  - [ ] JWT structure, signing (RS256), JWKS, validation, expiry, revocation strategies
- [ ] Resource server (`oauth2ResourceServer().jwt()`), OAuth2 client/login
- [ ] **Keycloak** as the IdP (or Spring Authorization Server)
- [ ] Multi-tenancy, API keys, mTLS between services
- [ ] Passkeys/WebAuthn (awareness), one-time tokens
- [ ] Testing: `@WithMockUser`, `jwt()` request post-processors

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 Log the security filter chain; send a bad JWT and trace the rejection
- [ ] 🟡 Keycloak org-per-tenant + roles + a JWT resource server
- [ ] 🔴 API keys (hashed, prefix lookup, rotation) as a custom `AuthenticationProvider`
- [ ] 🔴 Postgres RLS driven by the authenticated tenant; a cross-tenant attack suite
- [ ] ⚫ OAuth2 client for connectors (GitHub/Slack) with encrypted token storage + refresh

## 🧠 Cognitive tasks
- [ ] Draw Auth Code + PKCE from memory; explain what each parameter prevents
- [ ] Threat model (STRIDE) for API keys

## 🛰️ Orbit integration
- [ ] Multi-tenancy for orbit-api; the OAuth connectors in orbit-tools

> [!info] Go deeper
> ⚙️ [[Spring Internals]] · 🔒 [[Security Engineering]]

## Resources
- *Spring Security in Action* 2e (Spilcă) ⭐ · Spring Security reference docs
- *OAuth 2 in Action* · oauth.net · jwt.io · *API Security in Action* (Madden)
Related: [[Security Engineering]]
