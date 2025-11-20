# Beans

## Bean - Definition
The objects that are managed by the Spring IOC Container are called Beans.

## Bean scopes

**Bean scope** defines the lifecycle and visibility of a bean instance within the Spring IoC container—specifically, how many instances of a bean are created, and how they are shared or reused. The scope determines whether a single shared instance is used (singleton), a new instance is created for each request (prototype), or the bean is tied to a specific web request/session/application context.

Common bean scopes in Spring (important for exam questions):

- singleton (default) — one shared instance per Spring IoC container.
- prototype — a new instance each time requested from the container.
- request — one instance per HTTP request (web-aware contexts).
- session — one instance per HTTP session.
- application — one instance per ServletContext.
- websocket — one instance per WebSocket session.

Note: lifecycle callbacks are called for singleton beans by the container, but for prototype beans the container creates and injects them but does not manage the full lifecycle (destruction callbacks are not called automatically).

## Wiring and component scanning

- `@Component`, `@Service`, `@Repository`, `@Controller` — stereotype annotations used with component scanning to auto-detect and register beans.
- `@Configuration` and `@Bean` — define beans explicitly in Java configuration classes.
- `@Autowired` — performs injection by type (can be used on constructors, setters, fields).
- `@Qualifier` and `@Primary` — disambiguate when multiple candidate beans exist.
- `@Value` — inject simple property values from externalized configuration.

### Bean definition and creation methods

- Component scanning (`@Component`, `@Service`, etc.) — automatic detection and registration when component scanning is enabled (`@ComponentScan` or Spring Boot's auto-configuration).
- Java-based configuration — `@Configuration` classes with `@Bean` methods to create and configure beans programmatically.
- XML configuration — legacy but still sometimes seen in exam scenarios (bean definitions in `applicationContext.xml`).
- `FactoryBean` — custom factory objects that produce other bean instances (implement `FactoryBean<T>`).
- Programmatic registration — register beans directly in the `ApplicationContext`/`BeanDefinitionRegistry` (advanced).

### Bean names and aliases

- A bean has an identifier (name) and may have aliases. Stereotype annotations allow implicit names (e.g., `myService` for `@Service` on `MyService`). You can explicitly name beans with `@Component("name")` or `@Bean("name")`.

To set a bean scope use `@Scope("prototype")` or `@Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE)` on the class or `@Bean` method.

## Autowiring rules and common behaviors

- By default Spring resolves dependencies by type. If multiple beans match, `@Primary` or `@Qualifier` may be used to select the correct bean.
- Constructor injection is recommended; with a single constructor, Spring automatically uses it even without `@Autowired` (since Spring 4.3+).
- Circular dependencies: Spring can resolve circular dependencies for singleton beans using setter/field injection (through early references), but constructor-based cycles are not resolvable and will fail.

## Lifecycle and callbacks

- `@PostConstruct` / `@PreDestroy` — JSR lifecycle annotations called after initialization and before destruction.
- `InitializingBean` / `DisposableBean` — Spring interfaces providing `afterPropertiesSet()` and `destroy()` hooks.
- `BeanPostProcessor` — allows custom modification of new bean instances (useful for proxies, additional initialization).
- Lazy initialization: `@Lazy` delays bean creation until first requested.

### Typical bean lifecycle (simplified)

1. Bean definition is read from configuration (component scan / @Bean / XML).
2. Bean instance is instantiated.
3. Dependencies are injected (constructor/setter/field).
4. `BeanNameAware` / `BeanFactoryAware` callbacks are invoked (if implemented).
5. `BeanPostProcessor.postProcessBeforeInitialization` is called.
6. Initialization callbacks are invoked (`@PostConstruct`, `afterPropertiesSet()`, custom init-method).
7. `BeanPostProcessor.postProcessAfterInitialization` is called (proxying often happens here).
8. Bean is ready for use by the application.
9. On shutdown, destruction callbacks run for container-managed scopes (`@PreDestroy`, `destroy()`); prototype beans are not destroyed by the container automatically.

## Best practices (brief)

- Prefer `ApplicationContext` in real applications.
- Use constructor injection for mandatory dependencies and mark optional ones with setters or `@Nullable`.
- Prefer Java configuration (`@Configuration`) and component scanning for new code; know XML historically for exam scenarios.
- Avoid field injection when possible; it makes testing harder.

## Best practices (exam-focused)

- Prefer constructor injection for mandatory dependencies; use `@Autowired` on constructors only when necessary for readability.
- Avoid field injection in production code; it's harder to test and hides dependencies.
- Understand the runtime differences between singleton and prototype scopes and when destruction callbacks are invoked.
- Know the common annotations: `@Component`, `@Service`, `@Repository`, `@Controller`, `@Configuration`, `@Bean`, `@Autowired`, `@Qualifier`, `@Primary`, `@Value`, `@Lazy`.

## Minimal examples

Constructor injection with stereotype and configuration examples (kept small for exam revision):

```java
// A simple service
@Service
public class GreetingService {
		private final TimeService timeService;

		// Constructor injection — preferred
		public GreetingService(TimeService timeService) {
				this.timeService = timeService;
		}

		public String greet(String name) {
				return "Hello " + name + " — " + timeService.getTimeOfDay();
		}
}

// Java config
@Configuration
public class AppConfig {
		@Bean
		public TimeService timeService() {
				return new SystemTimeService();
		}
}
```

// Example: @Primary and @Qualifier

```java
@Configuration
public class DataConfig {
	@Bean
	@Primary
	public DataSource primaryDataSource() {
		return createHikari("jdbc:primary");
	}

	@Bean("reportDataSource")
	public DataSource reportDataSource() {
		return createHikari("jdbc:reports");
	}
}

@Service
public class ReportService {
	private final DataSource ds;

	// inject by name using @Qualifier
	public ReportService(@Qualifier("reportDataSource") DataSource ds) {
		this.ds = ds;
	}
}
```

## Exam tips

- Be ready to answer how Spring creates and injects beans, differences between injection types, and how `@Qualifier` and `@Primary` affect autowiring.
- Know which bean scopes are available and how lifecycle callbacks differ between singleton and prototype.
- Expect questions on circular dependency behavior and how to avoid or resolve it.
