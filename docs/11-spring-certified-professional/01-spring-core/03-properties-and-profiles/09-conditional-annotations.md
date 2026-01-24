# Conditional Bean Annotations

Conditional Spring bean annotations allow you to register beans only when certain conditions are met, giving you fine-grained control over bean creation based on environment, configuration, or classpath.

## Common Conditional Annotations and Examples:

1. **`@ConditionalOnProperty`**  
   Register a bean only if a specific property exists and optionally has a certain value.

```java
@Configuration
public class FeatureConfig {

    @Bean
    @ConditionalOnProperty(name = "feature.enabled", havingValue = "true")
    public FeatureBean featureBean() {
        return new FeatureBean();
    }
}
```

This bean is only created if `feature.enabled=true` in `application.properties`.

2. **`@ConditionalOnClass` and `@ConditionalOnMissingClass`**  
   Load a bean if a particular class is present or absent on the classpath.

```java
@Bean
@ConditionalOnClass(name = "com.example.OptionalLibrary")
public OptionalLibraryBean optionalBean() {
    return new OptionalLibraryBean();
}
```

3. **`@ConditionalOnBean` and `@ConditionalOnMissingBean`**  
   Create beans depending on the existence or absence of other beans.

```java
@Bean
@ConditionalOnBean(DataSource.class)
public JdbcTemplate jdbcTemplate(DataSource ds) {
    return new JdbcTemplate(ds);
}
```

4. **`@ConditionalOnExpression`**  
   Define beans with arbitrary Spring Expression Language (SpEL) conditions.

```java
@Bean
@ConditionalOnExpression("#{systemProperties['os.name'].toLowerCase().contains('windows')}")
public WindowsSpecificBean windowsBean() {
    return new WindowsSpecificBean();
}
```

5. **Custom Conditions with `@Conditional`**  
   Implement your own logic by creating a class implementing `Condition` interface and use `@Conditional`.

```java
public class MyCustomCondition implements Condition {
    @Override
    public boolean matches(ConditionContext context, AnnotatedTypeMetadata metadata) {
        // custom logic
        return true;
    }
}

@Bean
@Conditional(MyCustomCondition.class)
public MyBean myBean() {
    return new MyBean();
}
```

### Summary

Conditional annotations in Spring allow flexible bean registrations based on runtime environment, properties, classpath presence, or custom logic. They help build modular, environment-aware applications. You can combine these conditions for complex use cases.

This feature is extensively used in Spring Boot’s auto-configuration to enable optional features and integrations based on the runtime context.
