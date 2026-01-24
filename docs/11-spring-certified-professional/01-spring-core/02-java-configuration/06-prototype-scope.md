# Prototype Bean Scope

- The prototype bean scope in Spring means that a new instance of the bean is created every time it is requested from the Spring container. 
- This scope is commonly used for stateful beans, as each request or injection gets its own separate object.

## use case

Yes, you can use a Spring prototype-scoped bean to generate unique values like an OrderId. Every time you request a bean from the Spring container with prototype scope, you get a new instance. By adding a field for an OrderId (for example, a UUID or a sequence number) that is initialized in the constructor, each instance will have a unique value.

## Example

```java
import org.springframework.context.annotation.Scope;
import org.springframework.stereotype.Component;
import java.util.UUID;

@Component
@Scope("prototype")
public class OrderIdGenerator {
    private final String orderId;

    public OrderIdGenerator() {
        this.orderId = UUID.randomUUID().toString();
    }

    public String getOrderId() {
        return orderId;
    }
}
```

Each time you call `context.getBean(OrderIdGenerator.class)`, you receive a new object with a new order ID generated.[1]

**Note:** If you inject a prototype bean directly into a singleton bean, only one instance will be created and reused. To get a fresh instance for each request within a singleton, use `ObjectFactory` or `Provider`:

```java
@Autowired
private ObjectFactory<OrderIdGenerator> orderIdFactory;

public void createOrder() {
    OrderIdGenerator generator = orderIdFactory.getObject();
    System.out.println(generator.getOrderId());
}
```

This ensures you get a unique OrderId for each invocation.[1]

OR

Define the scope as shown below:

```java

package com.lousing.poc.util;

import org.springframework.context.annotation.Scope;
import org.springframework.context.annotation.ScopedProxyMode;
import org.springframework.stereotype.Component;

import java.util.UUID;

@Component
@Scope(value = "prototype", proxyMode = ScopedProxyMode.TARGET_CLASS)
public class OrderIdGenerator {
    private final String orderId = "ORDER-" + UUID.randomUUID().toString();

    public String getOrderId() {
        return orderId;
    }
}

```

Pay attention to the proxyMode