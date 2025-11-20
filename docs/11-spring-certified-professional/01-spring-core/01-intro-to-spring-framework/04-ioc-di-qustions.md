# IOC - DI Questions

## 1. What is Inversion of Control (IOC)?

**Answer:**
Inversion of Control is a design principle where the control of object creation and lifecycle management is transferred from application code to a framework. Instead of the application creating objects and managing dependencies, the IOC container handles this responsibility. This inverts the traditional flow where the application controls the framework.

**Key benefits:**
- Decouples components
- Improves testability
- Promotes loose coupling
- Simplifies code maintenance

---

## 2. Explain the difference between IOC and Dependency Injection (DI).

**Answer:**
- **IOC (Inversion of Control):** A broad principle where the framework controls the flow and object creation
- **DI (Dependency Injection):** A specific implementation of IOC that injects dependencies into objects rather than having objects create them

DI is a technique to achieve IOC. All DI is IOC, but not all IOC is DI.

---

## 2a. What are other techniques to achieve IOC besides Dependency Injection?

**Answer:**

1. **Service Locator Pattern:**
   ```java
   public class UserService {
       private ServiceLocator locator;
       
       public UserService(ServiceLocator locator) {
           this.locator = locator;
       }
       
       public void process() {
           UserRepository repository = locator.getService(UserRepository.class);
           // use repository
       }
   }
   ```
   - Objects request dependencies from a central registry
   - Less popular than DI
   - **Disadvantage:** Hidden dependencies, harder to test

2. **Factory Pattern:**
   ```java
   public class UserServiceFactory {
       public static UserService createUserService() {
           UserRepository repository = new UserRepository();
           return new UserService(repository);
       }
   }
   ```
   - Encapsulates object creation logic
   - Delegates creation to factory methods
   - Spring's `@Bean` methods are based on factory pattern

3. **Template Method Pattern:**
   ```java
   public abstract class BaseService {
       public final void execute() {
           Object dependency = createDependency();
           doWork(dependency);
       }
       
       protected abstract Object createDependency();
       protected abstract void doWork(Object dependency);
   }
   ```
   - Subclasses override methods to provide dependencies
   - Less flexible than DI

4. **Strategy Pattern:**
   ```java
   public class UserService {
       private AuthenticationStrategy strategy;
       
       public void setAuthStrategy(AuthenticationStrategy strategy) {
           this.strategy = strategy;
       }
   }
   ```
   - Objects receive different implementations at runtime
   - Allows behavior variation

5. **Event-Driven/Observer Pattern:**
   ```java
   public class EventBus {
       public void publish(Event event) {
           // notify all listeners
       }
   }
   ```
   - Components communicate through events
   - Reduces coupling between components

6. **Callback Functions:**
   ```java
   public void processUser(UserCallback callback) {
       UserRepository repository = new UserRepository();
       User user = repository.findById(1L);
       callback.onSuccess(user);
   }
   ```
   - Pass functions/callbacks to handle results
   - Common in functional programming

**Comparison with DI:**
- **Dependency Injection:** Most explicit, testable, and recommended
- **Service Locator:** Still hides dependencies, requires runtime lookup
- **Factory Pattern:** Good for complex creation logic, works well with DI
- **Others:** More specific use cases, often combined with DI

**Best Practice:** Dependency Injection is preferred in Spring applications as it's the most explicit and testable approach.

---

## 3. What are the three types of Dependency Injection?

**Answer:**

1. **Constructor Injection:**
   ```java
   public class UserService {
       private final UserRepository repository;
       
       public UserService(UserRepository repository) {
           this.repository = repository;
       }
   }
   ```
   - Dependencies are injected through constructor
   - Ensures immutability
   - Makes dependencies explicit
   - **Best for mandatory dependencies**

2. **Setter Injection:**
   ```java
   public class UserService {
       private UserRepository repository;
       
       @Autowired
       public void setRepository(UserRepository repository) {
           this.repository = repository;
       }
   }
   ```
   - Dependencies are injected through setter methods
   - Allows optional dependencies
   - More flexible but less type-safe
   - **Good for optional dependencies**

3. **Field Injection:**
   ```java
   public class UserService {
       @Autowired
       private UserRepository repository;
   }
   ```
   - Dependencies are injected directly into fields
   - Simple and concise
   - Less explicit about dependencies
   - **Not recommended - harder to test and can hide dependencies**

**Best Practice:** Constructor Injection is preferred for mandatory dependencies. Avoid field injection in production code due to testability concerns and hidden dependencies.

---

## 4. What are the resposibilities of Spring IOC Container?

**Answer:**
The Spring IOC Container is responsible for:
- Creating bean instances
- Configuring beans
- Managing bean lifecycle
- Resolving dependencies
- Managing bean scope

## 5. What are the two types of containers in Spring?
**Answer:**
Spring provides two types of containers:
1. **BeanFactory:** Basic container, lightweight
2. **ApplicationContext:** Advanced container with additional features like event publishing, i18n support

---

## 5. What is a Spring Bean?

**Answer:**
A Spring Bean is an object that is instantiated, assembled, and managed by the Spring IOC container. Beans are the backbone of Spring applications.

**Characteristics:**
- Managed by the container
- Configured in configuration files or annotations
- Can have dependencies injected
- Follow specific lifecycle callbacks
- Can be singleton, prototype, or other scopes

---

## 6. What are Bean Scopes in Spring?

**Answer:**

**Definition:** Bean scope defines the lifecycle and visibility of a bean instance within the Spring container. It determines how many instances of a bean are created and how long they live.

**Types of Bean Scopes:**

1. **Singleton (default):**
   - One instance per container
   - Shared across entire application
   - Best for stateless beans

   ```java
   @Component
   @Scope("singleton")
   public class SingletonBean { }
   ```

2. **Prototype:**
   - New instance every time requested
   - Each caller gets unique instance
   - Good for stateful beans

   ```java
   @Component
   @Scope("prototype")
   public class PrototypeBean { }
   ```

3. **Request (web-aware):**
   - One instance per HTTP request
   - Only available in web applications

4. **Session (web-aware):**
   - One instance per HTTP session
   - Maintains state across requests

5. **Global Session:**
   - One instance per global session
   - Used in Portlet applications
   - **Note:** Portlet applications are web applications using the JSR 168/286 standard (Java Portlet Specification defining portlet lifecycle, communication, and deployment); similar to session but across multiple portlets on a single page

6. **Application:**
   - One instance per ServletContext
   - Shared across entire application

---

## 7. Explain the difference between Singleton and Prototype scope.

**Answer:**

| Feature | Singleton | Prototype |
|---------|-----------|-----------|
| Instances | One per container | New per request |
| Creation | Lazy (by default) | Every time requested |
| Performance | Better (reused) | Lower (new objects) |
| State | Shared | Isolated |
| Thread Safety | Requires careful handling | Less critical |
| Use Case | Stateless services | Stateful objects |

---

## 8. How do you configure beans in Spring?

**Answer:**

1. **XML Configuration:**
   ```xml
   <bean id="userService" class="com.example.UserService">
       <constructor-arg ref="userRepository"/>
   </bean>
   ```

2. **Java Configuration (Recommended):**
   ```java
   @Configuration
   public class AppConfig {
       @Bean
       public UserRepository userRepository() {
           return new UserRepository();
       }
       
       @Bean
       public UserService userService(UserRepository repository) {
           return new UserService(repository);
       }
   }
   ```

3. **Annotation-based (Component Scanning):**
   ```java
   @Component
   public class UserService {
       @Autowired
       private UserRepository repository;
   }
   ```

---

## 9. What is Autowiring and explain the different modes.

**Answer:**
Autowiring automatically injects dependencies without explicit configuration.

**Autowiring Modes:**

1. **No (default):**
   - No automatic injection
   - Must specify dependencies explicitly

2. **ByName:**
   ```java
   @Autowired(required=false)
   private UserRepository userRepository; // matches bean name
   ```
   - Matches bean by property name

3. **ByType:**
   ```java
   @Autowired
   private UserRepository repository; // matches bean type
   ```
   - Matches bean by type
   - Fails if multiple beans of same type exist

4. **Constructor:**
   - Spring calls constructor with matching beans

5. **Default:**
   - Combination of constructor and byType

**Common Issue:** If multiple beans of same type exist, use `@Qualifier` annotation.

---

## 10. What is @Qualifier annotation and when do you use it?

**Answer:**
`@Qualifier` is used to disambiguate when multiple beans of the same type exist.

```java
@Service
public class UserService {
    private UserRepository repository;
    
    @Autowired
    public UserService(@Qualifier("primaryRepository") UserRepository repository) {
        this.repository = repository;
    }
}

@Repository("primaryRepository")
public class PrimaryUserRepository implements UserRepository { }

@Repository("secondaryRepository")
public class SecondaryUserRepository implements UserRepository { }
```

**Use Cases:**
- Multiple implementations of same interface
- Multiple beans of same type
- Disambiguating between similar beans

---

## 11. Explain Bean Lifecycle in Spring.

**Answer:**
Spring bean lifecycle has the following phases:

1. **Instantiation:** Bean instance created
2. **Populate Properties:** Dependencies injected
3. **Set Bean Name:** `BeanNameAware.setBeanName()` called
4. **Set Bean Factory:** `BeanFactoryAware.setBeanFactory()` called
5. **Post-Process Before Initialization:** `BeanPostProcessor.postProcessBeforeInitialization()`
6. **Initialize:** `afterPropertiesSet()` or `init-method` called
7. **Post-Process After Initialization:** `BeanPostProcessor.postProcessAfterInitialization()`
8. **Ready for Use**
9. **Destroy:** `destroy()` or `destroy-method` called

**Example:**
```java
@Component
public class UserService implements InitializingBean, DisposableBean {
    
    @PostConstruct
    public void init() {
        // called after properties set
    }
    
    @PreDestroy
    public void cleanup() {
        // called before destruction
    }
}
```

---

## 12. What is the difference between @Component, @Service, @Repository, and @Controller?

**Answer:**
All are specializations of `@Component` for different layers:

| Annotation | Layer | Purpose |
|------------|-------|---------|
| `@Component` | Generic | Generic component |
| `@Service` | Business Logic | Service layer beans |
| `@Repository` | Data Access | DAO/Repository layer |
| `@Controller` | Web | MVC controller |

```java
@Repository
public class UserRepository { }

@Service
public class UserService { }

@Controller
public class UserController { }
```

**Benefits:**
- Makes architecture clear
- Enables specific processing
- Better for AOP and exception translation

---

## 13. What happens if you define two beans with same name?

**Answer:**
Spring will throw `BeanDefinitionStoreException` or the later one will override the earlier one, depending on configuration:

```java
@Configuration
public class AppConfig {
    @Bean(name = "userService")
    public UserService userService1() {
        return new UserService();
    }
    
    @Bean(name = "userService")  // Will override previous bean
    public UserService userService2() {
        return new UserService();
    }
}
```

**Solutions:**
- Use different bean names
- Use `@Primary` to specify default
- Use `@Qualifier` to disambiguate

---

## 14. What is @Autowired(required=false)?

**Answer:**
`@Autowired(required=false)` makes dependency injection optional:

```java
@Service
public class UserService {
    @Autowired(required=false)
    private CacheService cacheService; // Won't fail if bean not found
    
    public void getUser(Long id) {
        if (cacheService != null) {
            return cacheService.getUser(id);
        }
        // fallback logic
    }
}
```

**Use Cases:**
- Optional features
- Plugin architecture
- Conditional functionality

---

## 15. Explain Circular Dependency and how Spring handles it.

**Answer:**
Circular dependency occurs when two or more beans depend on each other:

```java
@Component
public class ServiceA {
    @Autowired
    private ServiceB serviceB;
}

@Component
public class ServiceB {
    @Autowired
    private ServiceA serviceA;
}
```

**How Spring handles it:**
- Uses **object proxies** for singleton beans
- Constructor injection fails (cannot be resolved)
- Setter/field injection works via lazy initialization

**Solution:**
```java
@Component
public class ServiceA {
    @Autowired
    public void setServiceB(ServiceB serviceB) {
        this.serviceB = serviceB;
    }
}
```

Use setter injection instead of constructor injection for circular dependencies.

 