# About Beans

**Spring Beans** are the core components of the Spring Framework. Spring Beans are instances of classes that are created and managed by the Spring container.

Here's a simple example of a Spring Bean:

```java
@Component
public class Greeter {
    public String sayHello() {
        return "Hello!";
    }
}
```

In this example, the `Greeter` class is annotated with `@Component`, which makes it a Spring Bean. The Spring container will create an instance of the `Greeter` class and make it available for injection into other beans.

## **Spring Bean Lifecycle**

When a Spring Bean is created, it goes through several stages:

1. **Instantiation**: The Spring container creates an instance of the Bean class.
2. **Dependency Injection**: The Spring container injects dependencies into the Bean instance.
3. **Initialization**: The Spring container calls the Bean's `init-method` (if defined).
4. **Bean is Available**: The Bean is now available for use in the application.

When the application is shut down, the Spring container goes through the following stages:

1. **Bean is Destroyed**: The Spring container calls the Bean's `destroy-method` (if defined).
2. **Bean is Removed from Memory**: The Spring container removes the Bean instance from memory.

Here's an example of a Spring Bean with an `init-method` and a `destroy-method`:

```java
@Component
public class Greeter {
    public String sayHello() {
        return "Hello!";
    }

    @PostConstruct
    public void init() {
        System.out.println("Bean initialized");
    }

    @PreDestroy
    public void destroy() {
        System.out.println("Bean destroyed");
    }
}
```

In this example, the `Greeter` Bean has an `init-method` annotated with `@PostConstruct` and a `destroy-method` annotated with `@PreDestroy`.

## **Spring Bean Scopes**

Spring Beans can have different scopes, which determine how many instances of the Bean are created and managed by the Spring container. Here are some common scopes:

1. **Singleton**: A single instance of the Bean is created and shared across the application. This is the default scope.
2. **Prototype**: A new instance of the Bean is created every time it is requested. This scope is useful when the Bean has a high cost of creation or has a short lifespan.
3. **Request**: A new instance of the Bean is created for every HTTP request. This scope is useful when the Bean is specific to a single request and doesn't need to be shared across requests.
4. **Session**: A new instance of the Bean is created for every HTTP session. This scope is useful when the Bean is specific to a single session and doesn't need to be shared across sessions.
5. **Application**: A single instance of the Bean is created and shared across the entire application. This scope is useful when the Bean is a global configuration or utility.
6. **WebSocket**: A new instance of the Bean is created for every WebSocket connection. This scope is useful when the Bean is specific to a single WebSocket connection and doesn't need to be shared across connections.

Here's an example of using different scopes:

```java
// Singleton scope (default)
@Component
public class Greeter {
    public String sayHello() {
        return "Hello!";
    }
}

// Prototype scope
@Component
@Scope("prototype")
public class Greeter {
    public String sayHello() {
        return "Hello!";
    }
}

// Request scope
@Component
@Scope("request")
public class Greeter {
    public String sayHello() {
        return "Hello!";
    }
}
```

## **Spring Bean Annotations**

Spring provides several annotations that can be used to define the role of a Bean in the application. Here are some common annotations:

1. **@Component**: Marks a class as a Spring Bean. This is a generic annotation that can be used for any type of Bean.
2. **@Repository**: Marks a class as a data access object (DAO) that encapsulates the persistence logic for a particular domain model.
3. **@Service**: Marks a class as a service layer that encapsulates the business logic for a particular domain model.
4. **@Controller**: Marks a class as a web controller that handles HTTP requests and returns HTTP responses.
5. **@Configuration**: Marks a class as a configuration class that defines the Spring Bean definitions for the application.
6. **@Bean**: Marks a method as a factory method that returns a Spring Bean instance.
7. **@Value**: Injects a property value into a Bean instance.
8. **@Autowired**: Injects a dependency into a Bean instance.

Here's an example of using these annotations:

```java
// @Component
@Component
public class Greeter {
    public String sayHello() {
        return "Hello!";
    }
}

// @Repository
@Repository
public class UserRepository {
    public List<User> findAll() {
        // implementation
    }
}

// @Service
@Service
public class UserService {
    @Autowired
    private UserRepository userRepository;

    public List<User> findAll() {
        return userRepository.findAll();
    }
}

// @Controller
@Controller
public class UserController {
    @Autowired
    private UserService userService;

    @GetMapping("/users")
    public String findAllUsers(Model model) {
        model.addAttribute("users", userService.findAll());
        return "users";
    }
}
```
