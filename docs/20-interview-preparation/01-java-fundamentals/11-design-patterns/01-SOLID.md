The **SOLID principles** are five object-oriented design principles that help you write **clean, maintainable, extensible, and testable Java code**. They are especially relevant in Java because of its strong OOP focus (interfaces, inheritance, polymorphism).

Let’s go through each principle **with Java-centric explanations and examples**.

---

## 1. **S – Single Responsibility Principle (SRP)**

> **A class should have only one reason to change.**

### ❌ Violation

```java
class UserService {
    public void registerUser(User user) {
        // save user to DB
    }

    public void sendWelcomeEmail(User user) {
        // send email
    }
}
```

**Problems**

- Database logic and email logic are mixed
- Changing email logic forces modification of `UserService`

### ✅ Correct Design

```java
class UserRepository {
    public void save(User user) {
        // DB logic
    }
}

class EmailService {
    public void sendWelcomeEmail(User user) {
        // email logic
    }
}

class UserService {
    private final UserRepository userRepository;
    private final EmailService emailService;

    public UserService(UserRepository repo, EmailService email) {
        this.userRepository = repo;
        this.emailService = email;
    }

    public void registerUser(User user) {
        userRepository.save(user);
        emailService.sendWelcomeEmail(user);
    }
}
```

**Benefits in Java**

- Easier unit testing
- Clear separation of concerns
- Better package structuring

---

## 2. **O – Open/Closed Principle (OCP)**

> **Classes should be open for extension but closed for modification.**

### ❌ Violation

```java
class DiscountService {
    public double calculate(String type, double amount) {
        if (type.equals("FESTIVE")) {
            return amount * 0.8;
        }
        if (type.equals("NEW_YEAR")) {
            return amount * 0.7;
        }
        return amount;
    }
}
```

**Problem**

- Adding a new discount requires modifying existing code

### ✅ Correct Design (Using Polymorphism)

```java
interface Discount {
    double apply(double amount);
}

class FestiveDiscount implements Discount {
    public double apply(double amount) {
        return amount * 0.8;
    }
}

class NewYearDiscount implements Discount {
    public double apply(double amount) {
        return amount * 0.7;
    }
}
```

```java
class DiscountService {
    public double calculate(Discount discount, double amount) {
        return discount.apply(amount);
    }
}
```

**Benefits in Java**

- New behavior added via new classes
- Leverages interfaces and polymorphism
- Works well with Spring’s DI

---

## 3. **L – Liskov Substitution Principle (LSP)**

> **Subclasses should be replaceable for their base classes without breaking behavior.**

### ❌ Violation

```java
class Bird {
    public void fly() {
        System.out.println("Flying");
    }
}

class Penguin extends Bird {
    @Override
    public void fly() {
        throw new UnsupportedOperationException();
    }
}
```

**Problem**

- `Penguin` cannot behave like a `Bird`
- Breaks polymorphism

### ✅ Correct Design

```java
interface Bird {}

interface FlyingBird extends Bird {
    void fly();
}

class Sparrow implements FlyingBird {
    public void fly() {
        System.out.println("Flying");
    }
}

class Penguin implements Bird {
    // no fly method
}
```

**Key Java Insight**

- If you need to override a method to throw an exception → design is wrong
- Prefer interfaces over deep inheritance

---

## 4. **I – Interface Segregation Principle (ISP)**

> **Clients should not be forced to depend on methods they do not use.**

### ❌ Violation

```java
interface Worker {
    void work();
    void eat();
}
```

```java
class RobotWorker implements Worker {
    public void work() {}
    public void eat() {
        // meaningless
    }
}
```

### ✅ Correct Design

```java
interface Workable {
    void work();
}

interface Eatable {
    void eat();
}
```

```java
class HumanWorker implements Workable, Eatable {
    public void work() {}
    public void eat() {}
}

class RobotWorker implements Workable {
    public void work() {}
}
```

**Benefits in Java**

- Cleaner interfaces
- Avoids empty or dummy method implementations
- Improves API clarity

---

## 5. **D – Dependency Inversion Principle (DIP)**

> **High-level modules should not depend on low-level modules. Both should depend on abstractions.**

### ❌ Violation

```java
class MySQLDatabase {
    public void save(String data) {}
}

class OrderService {
    private MySQLDatabase database = new MySQLDatabase();

    public void processOrder(String order) {
        database.save(order);
    }
}
```

**Problems**

- Tight coupling
- Hard to test
- Hard to switch DB

### ✅ Correct Design

```java
interface Database {
    void save(String data);
}

class MySQLDatabase implements Database {
    public void save(String data) {}
}
```

```java
class OrderService {
    private final Database database;

    public OrderService(Database database) {
        this.database = database;
    }

    public void processOrder(String order) {
        database.save(order);
    }
}
```

**Why this is powerful in Java**

- Enables constructor injection
- Works seamlessly with Spring / CDI
- Makes mocking easy in unit tests

---

## SOLID Summary Table

| Principle | Key Idea                 | Java Feature Used       |
| --------- | ------------------------ | ----------------------- |
| SRP       | One responsibility       | Classes, packages       |
| OCP       | Extend without modifying | Interfaces, inheritance |
| LSP       | Substitutable subclasses | Polymorphism            |
| ISP       | Small focused interfaces | Interfaces              |
| DIP       | Depend on abstractions   | Interfaces, DI          |

---

## How SOLID Appears in Real Java Projects

- **Spring Boot**
  - `@Service`, `@Repository`, `@Controller` → SRP
  - Dependency Injection → DIP

- **Strategy Pattern** → OCP
- **Mockito / JUnit** → enabled by DIP & SRP
- **Clean Architecture / Hexagonal Architecture** → SOLID everywhere

---
