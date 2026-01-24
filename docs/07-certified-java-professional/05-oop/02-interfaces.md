# Interfaces

Interfaces in Java are way to achieve full abstraction and multiple inheritance. \
An interface is a reference type in Java, similar to a class but contains only
- contants
- method signatures
- default methods
- static methods and
- nested types

It can not contain instance fields or constructors.


In the early days of Java, interfaces were strictly "contracts"—they could only contain method signatures (the "what") but no implementation (the "how"). However, Java 8 changed this to allow interfaces to evolve without breaking existing code.

---

### 1. Default Methods

A **default method** allows you to add new functionality to an interface while maintaining backward compatibility. Classes that already implement the interface aren't forced to implement the new method; they just "inherit" the default behavior.

**Key Rule:** Use the `default` keyword.

```java
interface Vehicle {
    void drive(); // Standard abstract method

    // Default method: Classes don't HAVE to override this
    default void honk() {
        System.out.println("Beep beep!");
    }
}

class Car implements Vehicle {
    public void drive() {
        System.out.println("Car is driving...");
    }
    // honk() is automatically available here
}

```

---

### 2. Static Methods

A **static method** in an interface is identical to a static method in a class. It belongs to the interface itself and cannot be overridden by implementing classes. It is perfect for **utility or helper methods** that are relevant to the interface.

**Key Rule:** Call it using the Interface name (e.g., `Vehicle.getFuelType()`).

```java
interface Vehicle {
    static void checkEngine() {
        System.out.println("Engine is healthy.");
    }
}

// To call it:
Vehicle.checkEngine(); 

```

---

### Why were these added? (The "Evolution" Problem)

Before Java 8, if you added a new method to a popular interface (like `List`), **every single class** in the world that implemented `List` would break until they added that new method.

By adding `default` methods, Java creators were able to add things like `list.sort()` or `forEach()` to existing interfaces without breaking millions of lines of old code.

---

### Comparison Summary

| Feature | Default Method | Static Method |
| --- | --- | --- |
| **Keyword** | `default` | `static` |
| **Can be Overridden?** | Yes | No |
| **How to Call** | On the object instance (`myCar.honk()`) | On the interface (`Vehicle.checkEngine()`) |
| **Main Purpose** | Backward compatibility & Interface evolution | Utility/Helper methods |

### Important Note: "Multiple Inheritance"

If a class implements two interfaces that both have the same `default` method, Java will throw a compiler error because it doesn't know which one to use. You must manually override the method in your class to resolve the conflict:

```java
@Override
public void honk() {
    InterfaceA.super.honk(); // Explicitly choose A
}

```

Would you like to see the difference between a **Functional Interface** (which uses lambdas) and these standard interfaces?


