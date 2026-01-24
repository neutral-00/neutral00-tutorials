# Beans

The objects that are managed by the Spring IOC Container are called **Beans**.

**Key Point:** Spring **instantiates** these objects AND **wires** their dependencies automatically (IoC principle).

## Minimal Examples

### Constructor Injection with Stereotype + Configuration

```java
// 1. BEAN: Spring creates & manages this instance
@Service  // ← Spring: "Scan & register as bean named 'greetingService'"
public class GreetingService {
    private final TimeService timeService;  // ← Spring will inject this

    // 2. CONSTRUCTOR INJECTION: Spring finds TimeService bean & wires it here
    public GreetingService(TimeService timeService) {
        this.timeService = timeService;  // ✅ Fully wired by Spring
    }

    public String greet(String name) {
        return "Hello " + name + " — " + timeService.getTimeOfDay();
    }
}

// 3. BEAN DEFINITION: Spring creates this bean via @Configuration
@Configuration
public class AppConfig {
    @Bean  // ← Spring: "Create & manage SystemTimeService as 'timeService' bean"
    public TimeService timeService() {
        return new SystemTimeService();  // Spring instantiates & stores in container
    }
}
```

**Bean Flow (Spring Container):**

```
1. Scan → Finds @Service GreetingService → Creates bean 'greetingService'
2. Scan → Finds @Configuration → Calls timeService() → Creates bean 'timeService'
3. Wires → GreetingService constructor gets 'timeService' injected ✅
```

### @Primary and @Qualifier (Multiple Beans)

```java
@Configuration
public class DataConfig {
    @Bean
    @Primary  // ← Default choice when multiple DataSource beans exist
    public DataSource primaryDataSource() {
        return createHikari("jdbc:primary");
    }

    @Bean("reportDataSource")  // ← Explicit name for disambiguation
    public DataSource reportDataSource() {
        return createHikari("jdbc:reports");
    }
}

@Service
public class ReportService {
    private final DataSource ds;

    // @Qualifier overrides @Primary for explicit wiring
    public ReportService(@Qualifier("reportDataSource") DataSource ds) {
        this.ds = ds;  // ✅ Spring injects SPECIFIC reportDataSource bean
    }
}
```

**Bean Resolution Priority:**

```
@Qualifier("reportDataSource") → reportDataSource bean ✅
(Overrides @Primary)
↓
@Primary → primaryDataSource bean (default fallback)
↓
By type (ambiguous → fails)
```

## Bean Management Flow (Exam Essential)

```
1. REGISTRATION: @Service/@Bean → Spring registers in ApplicationContext
2. INSTANTIATION: Spring calls 'new Constructor()'
3. WIRING: Spring injects constructor parameters (looks up other beans)
4. INITIALIZATION: @PostConstruct → bean ready ✅
```

## Exam Tips

- **How beans created:** Component scanning (`@Service`) OR `@Bean` methods
- **Injection types:** Constructor (preferred) > Setter > Field (`@Autowired`)
- **`@Qualifier` wins** over `@Primary` → Explicit > Implicit
- **Scopes:** `singleton` (default), `prototype`, `request`, `session`
- **Circular deps:** Constructor injection fails → Use `@Lazy` or Setter injection
- **Lifecycle:** `@PostConstruct` (after wiring), `@PreDestroy` (before destroy)

**Memory trick:** `@Primary` = "default pick", `@Qualifier` = "specific pick" 🎯

```

[1](https://docs.spring.io/spring-framework/reference/core/beans/introduction.html)
```
