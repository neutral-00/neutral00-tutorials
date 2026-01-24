# IOC / DI — Short Q&A

## What is Inversion of Control (IOC)?

Inversion of Control is a design principle where a framework (the IOC container) manages object creation and wiring instead of application code. This improves decoupling and testability.

## IOC vs Dependency Injection (DI)

IOC is the principle; DI is the common technique that supplies an object's dependencies from the container. DI is the typical way to implement IOC in Spring.

## Other ways to achieve IOC

- Service Locator: runtime lookup (hides dependencies)
- Factory methods: centralized creation logic (used by `@Bean`)
- Patterns like Strategy, Template Method, events or callbacks — used for specific scenarios and often combined with DI

## Types of Dependency Injection

- Constructor Injection — preferred for required dependencies
- Setter Injection — useful for optional dependencies
- Field Injection — concise but discouraged for production (harder to test)

## Responsibilities of the Spring IOC container

- Instantiate and configure beans
- Resolve dependencies
- Manage bean lifecycle and scopes

## Containers: `BeanFactory` vs `ApplicationContext`

- `BeanFactory`: lightweight, minimal features
- `ApplicationContext`: full-featured (events, i18n, AOP integration) — used in most apps

## What is a Spring Bean?

A Spring Bean is an object managed by the IOC container (created, configured, and injected by Spring).

## Bean scopes (common ones)

- `singleton` (default): one instance per container — created eagerly by default
- `prototype`: new instance each request
- `request`, `session`, `application`, `globalSession` — web/portlet scopes for scoped lifecycles

## Singleton vs Prototype (summary)

- Singleton: shared, one instance per container, good for stateless services
- Prototype: a new instance each time, used for stateful objects

## Configuring beans

- XML: legacy option
- Java `@Configuration` / `@Bean`: recommended for explicit wiring
- Component scanning (`@Component`, `@Service`, `@Repository`, `@Controller`) with annotations

## Autowiring modes (brief)

- byType, byName, constructor; annotations `@Autowired`, `@Qualifier` help disambiguate when multiple beans exist.

## `@Qualifier` usage

Use `@Qualifier` to pick a specific bean when multiple candidates of the same type exist.

## Bean lifecycle (condensed)

Instantiation → Dependency injection → Aware callbacks (`BeanNameAware`, `BeanFactoryAware`) → `@PostConstruct` / `afterPropertiesSet()` → Post-processors → Ready → `@PreDestroy` / `destroy()`

Example:

```java
@Component
public class UserService {
    @PostConstruct
    public void init() { }

    @PreDestroy
    public void cleanup() { }
}
```

## Stereotype annotations

`@Component` is generic; `@Service`, `@Repository`, and `@Controller` are specialized for service, DAO, and web layers (and enable layer-specific processing).

## Duplicate bean names

If two beans share the same name, the later definition will override the earlier one when bean-definition overriding is enabled (DefaultListableBeanFactory allows this by default). If overriding is disabled, Spring throws a `BeanDefinitionOverrideException` (a `BeansException`). In Spring Boot you can control this with `spring.main.allow-bean-definition-overriding`.

Solutions: use unique names, `@Primary`, or `@Qualifier`, or change the overriding policy in configuration.

## Optional injection

`@Autowired(required = false)` makes a dependency optional — ensure you check for null before use.

## Circular dependencies

- Constructor injection cannot resolve circular dependencies
- Setter/field injection may work for singletons because Spring can use early references/proxies
- Best fix: refactor to remove the cycle or use setter injection as a last resort

---
