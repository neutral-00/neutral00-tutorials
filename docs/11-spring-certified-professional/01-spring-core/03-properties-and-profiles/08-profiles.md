# Spring Profiles

Spring Profiles allow you to define different sets of configuration and beans for different environments (e.g., development, test, production) within a Spring or Spring Boot application. This helps you activate environment-specific beans and properties easily and cleanly.

### How it works:
- You annotate configuration classes or beans with `@Profile("profileName")`.
- When the application runs with that profile active, only beans/configurations for that profile are loaded.
- Profiles can be specified in `application.properties`, programmatically, or via environment variables.

## Pre-requisite
1. create a git branch named `spring-profile-demo` in `$gp/pocs/poc-springboot`

## Step
1. Create a package named `config`
1. Inside it create `CacheConfig.java` as

```java
@Configuration
public class CacheConfig {

    @Bean
    @Profile("dev")
    public Cache devCache(){
        // Configure and return the development DataSource
        System.out.println("Development cache configured");
        return new ConcurrentMapCache("lousingCache");
    }

    // cache config for prod
    @Bean
    @Profile("prod")
    public Cache prodCache() {
        // Configure and return the production DataSource
        System.out.println("Production Cache configured");
        return null; // Replace with actual production cache implementation like RedisCache
    }
}

```
1. Activate profile in `application.properties`:

```properties
spring.profiles.active=dev
```

Or via command line:

```
java -jar app.jar --spring.profiles.active=prod
```

You can also have profile-specific properties files named like:

- `application-dev.properties`
- `application-prod.properties`

Spring will load the relevant file based on the active profile.

This approach cleanly separates environment configs and allows flexible, maintainable multi-environment management.
