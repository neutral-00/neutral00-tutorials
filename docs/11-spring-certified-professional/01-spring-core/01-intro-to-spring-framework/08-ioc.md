# Inversion of Control (IoC)

Inversion of Control is a design principle where the control of object creation and lifecycle management is transferred from application code to a framework.

Here we talking 2 things here

1. **creation** = Framework creates your objects (beans)
2. **management of objects and their dependencies** = Framework injects dependencies

## Quick Validation Example

```java
// 1. Declaration only (IoC principle)
@Component
class OrderService {
    public OrderService(EmailService email) { }  // No new EmailService(), just declared
}

// 2. Spring handles BOTH:
//    - Instantiation: new EmailServiceImpl()
//    - Wiring: injects into OrderService constructor
```
