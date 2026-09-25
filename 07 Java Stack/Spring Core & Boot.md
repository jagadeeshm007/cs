---
tags: [java, spring]
phase: 2
---
# 🌱 Spring Core & Spring Boot (target: Boot 4.x / Framework 7)

> [!tip] The secret to Spring mastery
> Spring is not magic. It's **reflection + proxies + conventions**. Once you understand IoC, bean post-processors, AOP proxies, and auto-configuration, every annotation becomes readable.

## Core → Advanced
### Spring Framework core
- [ ] IoC & DI: constructor injection, `@Component` scanning vs `@Bean` config
- [ ] Bean scopes, lifecycle, `BeanPostProcessor`, `BeanFactoryPostProcessor`
- [ ] `ApplicationContext`, events (`ApplicationEventPublisher`, `@TransactionalEventListener`)
- [ ] AOP: JDK dynamic proxy vs CGLIB, **self-invocation pitfall** (why `@Transactional` sometimes doesn't work)
- [ ] SpEL, `Environment`, property sources

### Spring Boot
- [ ] Auto-configuration: `@Conditional*`, how to read the conditions report (`--debug`)
- [ ] Externalized config, `@ConfigurationProperties` (typed, validated), profiles
- [ ] Starters; writing your own starter (great interview talking point)
- [ ] Spring MVC: `DispatcherServlet` flow, controllers, validation (`@Valid`), `@ControllerAdvice`, `ProblemDetail`
- [ ] `RestClient` (sync), `WebClient`, HTTP interface clients (`@HttpExchange`)
- [ ] Virtual threads (`spring.threads.virtual.enabled=true`)
- [ ] WebFlux/Reactor: understand it and know when it's worth it (rarely, now that virtual threads exist)
- [ ] Actuator: health, metrics (Micrometer), info, graceful shutdown
- [ ] Observability: Micrometer + OpenTelemetry tracing
- [ ] **Spring Modulith**: enforce module boundaries in a modular monolith ⭐
- [ ] Testing: `@SpringBootTest`, slices (`@WebMvcTest`, `@DataJpaTest`), Testcontainers with `@ServiceConnection`
- [ ] Docker Compose support, Buildpacks / layered jars, GraalVM native images, CDS
- [ ] Scheduling, async (`@Async`), caching abstraction (`@Cacheable` + Redis)

## 🧪 Labs (🟢 warm-up → 🟡 core → 🔴 hard → ⚫ boss)
- [ ] 🟢 Print the conditions report; override an auto-configured bean
- [ ] 🟡 A `BeanPostProcessor` logging creation time and proxy type for every bean
- [ ] 🔴 **Mini DI container** from scratch (W5 lab): scanning, constructor injection, cycle detection, a JDK-proxy `@Timed`
- [ ] 🔴 A custom starter: `orbit-idempotency-spring-boot-starter` with auto-config + conditions + tests
- [ ] ⚫ Step through `refresh()` and `DispatcherServlet.doDispatch()`; write the sequence from memory

## 🧠 Cognitive tasks
- [ ] Predict: does `@Transactional` apply in 5 tricky snippets? (self-call, private, final, `@Async`, interface proxy) Then verify
- [ ] Code archaeology: how does `@ConditionalOnMissingBean` let your bean win?

## 🛰️ Orbit integration
- [ ] orbit-api, orbit-knowledge, and orbit-tools are Spring Boot services
- [ ] Spring Modulith boundaries in orbit-api

> [!info] Go deeper
> ⚙️ [[Spring Internals]] · 🧩 [[GoF Patterns (Java & Go)]] · [[Enterprise & DDD Patterns]]

## Resources
- spring.io guides + reference docs ⭐ · **Spring Academy** (free courses) ⭐
- *Spring Start Here* (Spilcă) · *Spring in Action* 6e (Walls)
- YouTube: Dan Vega, Josh Long (*Spring Tips*), Laurențiu Spilcă
- Baeldung (reference)

## Interview questions #interview-q
- How does auto-configuration work?
- Why doesn't `@Transactional` work on a private/self-invoked method?
- Bean scopes? Circular dependencies: why they're bad, and how Boot handles them now?
- Filter vs Interceptor vs AOP?
