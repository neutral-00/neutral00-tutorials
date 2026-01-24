# Abstract Classes vs Interfaces

In Java, both **abstract classes** and **interfaces** are used to achieve abstraction, but they have significant differences in their usage and functionality. Let’s explore their features and differences.

---

## 1. Abstract Classes

An **abstract class** is a class that cannot be instantiated and may contain abstract methods (methods without a body) as well as concrete methods (methods with a body).

### Key Points:

- Declared using the `abstract` keyword.
- Can have both abstract and concrete methods.
- Can have instance variables and constructors.
- Supports single inheritance (a class can extend only one abstract class).

### Example:

```java
abstract class Animal {
    String name;

    // Abstract method
    abstract void sound();

    // Concrete method
    void eat() {
        System.out.println(name + " is eating.");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("The dog barks.");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myDog = new Dog();
        myDog.name = "Buddy";
        myDog.sound();
        myDog.eat();
    }
}
```

## 2. Interfaces

An **interface** is a reference type in Java, similar to a class, that can contain only constants, method signatures, default methods, static methods, and nested types. Interfaces cannot contain instance fields or constructors.

### Key Points:

- Declared using the `interface` keyword.
- Can have only abstract methods (until Java 7) or
- after Java 8+ it can have abstract methods, default methods, and static methods.
- Cannot have instance variables or constructors.
- Supports multiple inheritance (a class can implement multiple interfaces).

### Example:

```java
interface Animal {
    void sound(); // Abstract method

    // Default method (Java 8+)
    default void eat() {
        System.out.println("This animal is eating.");
    }
}

class Dog implements Animal {
    @Override
    public void sound() {
        System.out.println("The dog barks.");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal myDog = new Dog();
        myDog.sound();
        myDog.eat();
    }
}
```

## 3. Comparison Table

| Feature          | Abstract Class                              | Interface                                                                     |
| ---------------- | ------------------------------------------- | ----------------------------------------------------------------------------- |
| Declaration      | `abstract` keyword                          | `interface` keyword                                                           |
| Methods          | Can have both abstract and concrete methods | Only abstract methods (prior to Java 8); default and static methods (Java 8+) |
| Variables        | Can have instance variables                 | Only `public static final` constants                                          |
| Inheritance      | Supports single inheritance                 | Supports multiple inheritance                                                 |
| Constructors     | Can have constructors                       | Cannot have constructors                                                      |
| Access Modifiers | Can have any access modifier for methods    | Methods are implicitly `public`                                               |

## 4. FAQs

### 1. Is it possible to have an abstract class without any abstract method?

Yes

```java
abstract class Vehicle {
    void start() {
        System.out.println("Vehicle is starting...");
    }
}

class Car extends Vehicle {
    void drive() {
        System.out.println("Car is driving...");
    }
}

public class Main {
    public static void main(String[] args) {
        Car myCar = new Car();
        myCar.start(); // Inherited from abstract class
        myCar.drive();
    }
}

```

---

### 2. Why would abstract class have a constructor?

It's a common point of confusion, but the short answer is that an abstract class's constructor is meant for **initialization**, not **instantiation**. Even though you can't create an object of an abstract class directly, its constructor is always called when a concrete subclass is instantiated.

Here's why:

- **Initialization of Shared State:** Abstract classes can have instance variables and methods that are shared by all of their subclasses. These instance members often need to be initialized to a starting state. The abstract class's constructor is the perfect place to do this. When a child class is instantiated, it implicitly (or explicitly using `super()`) calls the abstract parent's constructor to set up that shared, initial state. This prevents you from having to repeat the same initialization logic in every single subclass.

  **Analogy**: Think of a `Car` abstract class with a `color` instance variable. All cars have a color, so you can define a constructor in the abstract `Car` class to initialize this variable. When you create an object of a concrete subclass like `Sedan` or `SUV`, the `Sedan` or `SUV` constructor will first call the `Car` constructor to set the `color` before performing its own specific initialization.

- **Enforcing a "Contract":** A constructor in an abstract class can enforce that certain parameters are passed from the subclass to ensure proper initialization. If a field in the abstract class is crucial for its functionality, a constructor can make sure that a subclass provides that necessary information. This promotes good design and prevents subclasses from being created with incomplete or invalid states.

In essence, a constructor in an abstract class is not for building an object of the abstract type, but rather for **helping** to build a **complete** object of a concrete subclass.

---

### 3. Discuss the role of `default` keyboard in a Java Interface?

**Quick Answer:**  
The `default` keyword in Java interfaces (introduced in Java 8) allows you to provide a **method implementation inside an interface**, so classes implementing the interface don’t have to override it unless they want to. This was added to support **API evolution** and **backward compatibility**.

---

#### 🧩 Why `default` Was Introduced

- **Before Java 8**: Interfaces could only have abstract methods. Adding a new method to an interface would break all existing implementations.
- **Java 8 onward**: `default` methods let you add new functionality to interfaces without forcing all implementing classes to change.
- **Goal**: Enable features like **Streams, Lambdas, and functional programming** while keeping older code intact.

#### 🔑 Characteristics of Default Methods

- Declared with the `default` keyword inside an interface.
- Provide a **concrete implementation**.
- Can be **overridden** by implementing classes.
- Cannot override `Object` methods (like `equals`, `hashCode`, `toString`).
- Can coexist with abstract methods, static methods, and constants inside an interface.

#### 📌 Example

```java
interface Vehicle {
    void start(); // abstract method

    default void honk() {
        System.out.println("Honking...");
    }
}

class Car implements Vehicle {
    @Override
    public void start() {
        System.out.println("Car started");
    }
    // honk() is inherited unless overridden
}

public class Main {
    public static void main(String[] args) {
        Vehicle car = new Car();
        car.start(); // Car started
        car.honk();  // Honking...
    }
}
```

---
