# Spring Configurations

How does the Spring IOC container know which classes should be instantiated as beans?



## Spring Configuration - Definition

Spring configuration defines how the IoC container discovers, creates, and wires beans. It tells the container which classes to instantiate, how to inject dependencies, and how to apply additional settings (scope, lifecycle, etc.).

Spring supports several configuration styles:

- **Java-based configuration**: Use `@Configuration` classes and `@Bean` methods to define beans programmatically.
- **Annotation-based configuration**: Use stereotype annotations (`@Component`, `@Service`, `@Repository`, `@Controller`) and enable component scanning with `@ComponentScan`.
- **XML-based configuration**: Define beans and wiring in XML files (e.g., `applicationContext.xml`). Still seen in legacy projects and on the exam.

### Java-based configuration example
```java
@Configuration
public class AppConfig {
	@Bean
	public UserService userService() {
		return new UserServiceImpl();
	}
}
```

### Annotation-based configuration example
```java
@Component
public class UserServiceImpl implements UserService {
	// ...
}

@Configuration
@ComponentScan(basePackages = "com.example.app")
public class AppConfig {}
```

### XML-based configuration example
```xml
<beans xmlns="http://www.springframework.org/schema/beans"
	   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	   xsi:schemaLocation="http://www.springframework.org/schema/beans
	   http://www.springframework.org/schema/beans/spring-beans.xsd">
	<bean id="userService" class="com.example.app.UserServiceImpl"/>
</beans>
```

### Component scanning
- Spring can automatically detect and register beans using classpath scanning. Enable with `@ComponentScan` (Java) or `<context:component-scan>` (XML).

### Externalized configuration
- Use `application.properties` or `application.yml` to externalize settings. Inject values with `@Value` or `@ConfigurationProperties`.

### Profiles
- Use `@Profile` to define beans for specific environments (dev, test, prod). Activate with `spring.profiles.active` property.

### Exam tips
- Know the differences and use-cases for Java, annotation, and XML configuration.
- Be able to recognize and write minimal examples for each style.
- Understand how component scanning works and how to limit it to specific packages.
- Know how to use externalized configuration and profiles for environment-specific beans.

### Hands-on
1. For Java Configurations demo check out `$gp/pocs/poc-greetings`
