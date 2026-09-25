---
tags: [internals, java, spring]
week: W5–W7
---
# 🌱 Spring Internals (important parts only)

## 1. Startup: `SpringApplication.run()` → `refresh()`
1. Create the `Environment` (property sources: args, env vars, `application.yml`, profiles)
2. Create the `ApplicationContext`
3. **`refresh()`** (`AbstractApplicationContext`) ⭐:
   - `invokeBeanFactoryPostProcessors` → **`ConfigurationClassPostProcessor`** parses `@Configuration`, `@ComponentScan`, `@Import`, `@Bean` → registers **BeanDefinitions** (recipes, not objects yet)
   - Auto-configuration is imported here (see §3)
   - `registerBeanPostProcessors` (e.g. `AutowiredAnnotationBeanPostProcessor`, the AOP auto-proxy creator)
   - `finishBeanFactoryInitialization` → instantiate all non-lazy singletons
   - `onRefresh` → start the embedded web server (Tomcat/Netty)
   - `finishRefresh` → publish `ContextRefreshedEvent`; `ApplicationReadyEvent` comes later

## 2. Bean lifecycle (`AbstractAutowireCapableBeanFactory.doCreateBean`)
**Instantiate** (constructor resolution) → **populate** (field/setter injection) → **Aware callbacks** → `BeanPostProcessor.before` → `@PostConstruct` / `afterPropertiesSet` / init-method → **`BeanPostProcessor.after` ← AOP proxies are created here** → ready → on shutdown, `@PreDestroy`
- The singleton registry has 3 caches (singletons, early references, factories) to resolve circular setter/field references. **Circular references are disallowed by default** in modern Boot → use constructor injection and redesign

## 3. Auto-configuration
- `@SpringBootApplication` = `@Configuration` + `@ComponentScan` + `@EnableAutoConfiguration`
- `AutoConfigurationImportSelector` (a *deferred* import selector, so it runs after your config) loads the class names listed in `META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports`
- Each auto-config is guarded by **conditions**: `@ConditionalOnClass`, `@ConditionalOnMissingBean` (**your bean wins**), `@ConditionalOnProperty`…
- Debug with `--debug` (conditions report) or `/actuator/conditions`

## 4. AOP & proxies
- A proxy wraps your bean: **CGLIB subclass** (Boot default) or **JDK dynamic proxy** (interfaces)
- Calls go proxy → interceptor chain (advisors) → target
- **Self-invocation (`this.method()`) bypasses the proxy** → `@Transactional`, `@Async`, `@Cacheable` silently don't apply. Final/private methods can't be proxied
- `@Transactional` → `TransactionInterceptor` → `PlatformTransactionManager.getTransaction()` → binds the connection/EntityManager to a **ThreadLocal** (`TransactionSynchronizationManager`) → commit/rollback. By default it **rolls back only on unchecked exceptions**

## 5. Web request flow (Spring MVC)
Tomcat NIO connector accepts → worker thread (or a virtual thread) → **servlet filter chain** (incl. `DelegatingFilterProxy` → **`FilterChainProxy`** → Security filters) → **`DispatcherServlet.doDispatch()`** → `HandlerMapping` (finds the controller method) → `HandlerInterceptor.preHandle` → `HandlerAdapter` → **argument resolvers** + `HttpMessageConverter` (Jackson) → your controller → return value handlers → message converter writes the response → exceptions go to `HandlerExceptionResolver` / `@ControllerAdvice`

## 6. Spring Security internals
- `SecurityContextHolder` (ThreadLocal by default) holds the `Authentication`
- The filter order matters: … → `BearerTokenAuthenticationFilter` → `JwtAuthenticationProvider` → `JwtDecoder` (JWKS fetched and cached) → `AuthorizationFilter`
- `ProviderManager` iterates `AuthenticationProvider`s; method security = AOP around `@PreAuthorize`

## 7. Spring Data JPA & Hibernate
- Repository interfaces → runtime **proxies**; query methods are parsed from method names (`PartTree`)
- **Persistence context** = first-level cache + identity map + **dirty checking** (snapshot comparison at flush)
- Flush order via the action queue (inserts → updates → deletes); `FlushMode.AUTO` flushes before queries
- Lazy associations = proxies/bytecode-enhanced fields → `LazyInitializationException` outside a transaction; N+1 appears when you iterate over them

## 🔬 Prove it
- [ ] Breakpoint in `AbstractApplicationContext.refresh()` and `doCreateBean()`; write down the order for your app's beans
- [ ] Write a `BeanPostProcessor` that logs each bean's creation time and whether it's a proxy (`AopUtils.isAopProxy`)
- [ ] Reproduce the `@Transactional` self-invocation bug; fix it 3 ways (separate bean, self-injection, `TransactionTemplate`)
- [ ] Override an auto-configured bean (e.g. `ObjectMapper`) and confirm in the conditions report
- [ ] Log the Security filter chain at startup; send a request with a bad JWT and trace which filter rejects it
- [ ] Enable Hibernate statistics; show dirty checking issuing an UPDATE without calling `save()`
- [ ] **Lab**: build a mini DI container → [[Assignments - Phase 2]]

## Interview questions #interview-q
Bean lifecycle · how auto-config works · why `@Transactional` fails on self-calls · JDK vs CGLIB proxies · the request flow through `DispatcherServlet` · how Spring Security validates a JWT · dirty checking · the N+1 root cause
