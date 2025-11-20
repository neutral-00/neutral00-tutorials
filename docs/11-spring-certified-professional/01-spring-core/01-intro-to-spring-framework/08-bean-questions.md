# Sample Exam Questions Around Beans

### Q. Which areas beans can be autowired on?
Answer: Properties (setters), Fields, Constructors, and Methods (including configuration methods).

### Q. What are the scopes of beans in a Web Context in Spring?
Answer: singleton, prototype, request, session, application, and websocket (in modern Spring). In legacy Spring, also globalSession (for Portlet applications).

### Q. Given a file config.properties, how would you configure it correctly using the `@PropertySource` annotation in the code given below?
```java
@Configuration
public class PropertiesWithJavaConfig {
    @Bean
    public static PropertySourcesPlaceholderConfigurer propertySourcesPlaceholderConfigurer() {
        return new PropertySourcesPlaceholderConfigurer();
    }
}
```
Answer: use `@PropertySource("classpath:config.properties")` as in below code.
```java
@Configuration
@PropertySource("classpath:config.properties")
public class PropertiesWithJavaConfig {
    @Bean
    public static PropertySourcesPlaceholderConfigurer propertySourcesPlaceholderConfigurer() {
        return new PropertySourcesPlaceholderConfigurer();
    }
}

Note: `@PropertySource("classpath:config.properties")` expects the file to be available on the application's classpath. In a typical Maven/Gradle project place `config.properties` under `src/main/resources/` so it is copied to the classpath root at build time. You can also store it in a subfolder (e.g. `classpath:config/config.properties`) or load external files using `file:/path/to/config.properties`.

Exam tip: In Spring Boot us e `application.properties` or `application.yml` under `src/main/resources/` for conventional configuration; custom property files still belong on the classpath or can be loaded from external locations.
```

### Q. You want to add a single entry to your web.xml and deal entirely with the application context file for managing you web security filter beans to avoid clutter. How would you do so?
Answer: use `FilterChainProxy` (Spring Security's DelegatingFilterProxy) as shown in the sample `web.xml` below:
```xml
<filter>
    <filter-name>springSecurityFilterChain</filter-name>
    <filter-class>org.springframework.web.filter.DelegatingFilterProxy</filter-class>
</filter>
<filter-mapping>
    <filter-name>springSecurityFilterChain</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

### Q. You have multiple application context in your project. Which bean scope will act at singleton per ApplicationContext?
Answer: singleton (the default scope). Each ApplicationContext maintains its own singleton instances; there is no cross-context singleton.

### Q. An application contains a number of packages to function. You scan the packages and sub-packages to search for a few components/beans. To do so, you used `@Beans` which didn't result in any significant results. How should you san the packages?
Answer: Use the `@ComponentScan` annotation with the `@Configuration` annotation as shown below:
```java
@Configuration
@ComponentScan(basePackages = {"com.example.package1", "com.example.package2"})
public class AppConfig {}
```

### Given the following custom auto configuration:
```java
@Configuration
public class AutoCarConfig {
    @Bean
    @ConditionalOnMissingBean
    public Car getCar() {
        return new Brand1();
    }
}
// and the following configuration class:
@Configuration
public class CarConfig() {
    @Bean
    public Car getCar() {
        return new Brand2();
    }
}
```
Which implementation will be injected into myCar within the CarService class?
```java
@Service
public class CarService {
    @Inject
    private Car myCar;
}
```
Answer: The Brand2 implementation. Because a bean of type Car is defined in CarConfig, it overrides the conditional bean in AutoCarConfig.

### Q. What are some of the different bean autowiring modes in a legacy Spring Application that uses the XML configuration method?
Answer: no (default), byName, byType, constructor, and autodetect (deprecated).

### Q. How will you annotate a bean holding some business logic?
Answer: `@Service` (for business logic), or `@Component` (generic stereotype).

### Q. The following code was built with the help of view resolvers, where you mixed different technologies together in an application
```xml
<bean id="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver">
    <property name="basename" value="views" />
    <property name="defaultParentView" value="parentView" />
</bean>
```
During execution, the code produces an error on line 2. Why?

Answer: The `basename` property is not supported by `InternalResourceViewResolver`; it is a property of `ResourceBundleViewResolver`. Use the correct view resolver for the property.

### Q. Consider the following bean definition:
```java
@Bean
public JdbcTemplate(DataSource dataSource) {
    JdbcTemplate jdbcTemplate = new JdbcTemplate(datasource);
    return jdbcTemmplate;
}
```
You forget to set an exception translator by calling: `jdbcTemplate.setExceptionTranlator(...)`. If you wite and execute a malformed SQL query with the jdbcTemplate, what is the default behavior?


Answer: Spring's `JdbcTemplate` automatically detects and applies a suitable SQLExceptionTranslator if configured with a DataSource.
JdbcTemplate uses `SQLErrorCodeSQLExceptionTranslator` by default and would translate the exception.
---

## Additional Questions to Cover Full Concept

### Q. What is a FactoryBean in Spring?
Answer: A `FactoryBean` is a special bean that, instead of exposing itself as a bean, exposes the object returned by its `getObject()` method. Used for advanced bean creation logic.

### Q. How do you define a bean as lazy-initialized?
Answer: Use `@Lazy` on the bean class or `@Bean` method, or set `lazy-init="true"` in XML. The bean will be created only when first requested.

### Q. How do you specify a primary bean when multiple candidates exist?
Answer: Use `@Primary` on the preferred bean or `<bean primary="true">` in XML. Spring will use this bean for autowiring unless a `@Qualifier` is specified.

### Q. How do you define an alias for a bean?
Answer: Use the `@Component("aliasName")` or `@Bean(name = {"mainName", "alias1", "alias2"})` syntax, or `<alias>` in XML.

### Q. What is the default bean scope in Spring?
Answer: singleton — one shared instance per container.

### Q. How can you make a bean prototype scoped?
Answer: Use `@Scope("prototype")` on the bean class or `@Bean` method, or set `scope="prototype"` in XML.

### Q. What is the lifecycle of a Spring bean?
Answer: Instantiation → Dependency Injection → Aware interfaces → BeanPostProcessors (before init) → Initialization callbacks → BeanPostProcessors (after init) → Ready for use → Destruction callbacks (if applicable).

### Q. How do you inject values from properties files into beans?
Answer: Use `@Value("${property.name}")` on fields, setters, or constructor parameters, and ensure a `PropertySourcesPlaceholderConfigurer` is configured.

### Q. How do you create a bean programmatically at runtime?
Answer: Use the `ConfigurableApplicationContext`'s `getBeanFactory().registerSingleton()` or `registerBeanDefinition()` methods.

### Q. What is the difference between `@Component`, `@Service`, `@Repository`, and `@Controller`?
Answer: All are stereotypes for auto-detection, but indicate intent: `@Component` (generic), `@Service` (business logic), `@Repository` (persistence/DAO, adds exception translation), `@Controller` (web MVC controller).

### Q. When do we get `org.springframework.beans.factory.NoUniqueBeanDefinitionException`?
Answer: This exception is thrown when the container finds more than one bean of the required type and cannot decide which one to inject or return. Common situations:

- Autowiring by type (e.g. `@Autowired` on a single-valued dependency) when multiple candidate beans of that type exist and neither `@Primary` nor `@Qualifier` is present.
- Calling `applicationContext.getBean(SomeType.class)` when more than one bean implements `SomeType`.

How to resolve:

- Use `@Primary` on the preferred bean.
- Use `@Qualifier("beanName")` to select a specific bean.
- Inject by name (e.g., `@Resource("beanName")`) or inject the exact bean type.
- Inject a collection (`List<SomeType>` or `Map<String, SomeType>`) if you need all candidates.
- Reduce the number of candidate beans or make one bean more specific.

Exam tip: the exception indicates a type ambiguity — the container needs extra information (primary/qualifier/name) to resolve the dependency.

### Example — reproducing and fixing NoUniqueBeanDefinitionException

Problematic configuration (will cause NoUniqueBeanDefinitionException at injection time):

```java
public interface Processor { void process(); }

public class VisaProcessor implements Processor { public void process() { /*...*/ } }
public class MasterProcessor implements Processor { public void process() { /*...*/ } }

@Configuration
public class ProcessorConfig {
    @Bean
    public Processor visaProcessor() {
        return new VisaProcessor();
    }

    @Bean
    public Processor masterProcessor() {
        return new MasterProcessor();
    }
}

@Service
public class PaymentService {
    // causes NoUniqueBeanDefinitionException because two Processor beans exist
    @Autowired
    private Processor processor;
}
```

Typical error message:

```
org.springframework.beans.factory.NoUniqueBeanDefinitionException: No qualifying bean of type 'com.example.Processor' available: expected single matching bean but found 2: visaProcessor, masterProcessor
```

Fix 1 — use @Qualifier (select bean by name):

```java
@Service
public class PaymentService {
    private final Processor processor;

    public PaymentService(@Qualifier("visaProcessor") Processor processor) {
        this.processor = processor;
    }
}
```

Fix 2 — mark one bean as @Primary (prefer this bean when multiple candidates exist):

```java
@Bean
@Primary
public Processor visaProcessor() { return new VisaProcessor(); }
```

Fix 3 — inject all candidates as a collection if you need to handle multiple implementations:

```java
@Service
public class PaymentService {
    private final List<Processor> processors;

    public PaymentService(List<Processor> processors) {
        this.processors = processors; // contains visaProcessor and masterProcessor
    }
}
```

Other options: use `@Resource("beanName")` to inject by name, or reduce the number of candidate beans.



