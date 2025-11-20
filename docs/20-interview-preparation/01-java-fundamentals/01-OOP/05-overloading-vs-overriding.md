# Overloading vs Overriding

In Java, **method overloading** and **method overriding** are two important concepts that allow flexibility and reusability in object-oriented programming. Let’s explore their differences and use cases.

---

## 1. Method Overloading
Method overloading allows multiple methods in the same class to have the same name but different parameter lists.

### Key Points:
- Happens **within the same class**.
- Methods must have the **same name** but **different parameter types, order, or number**.
- Return type can be different but is not sufficient to distinguish methods.
- It is an example of **compile-time (static) polymorphism**.

### Example:
```java
class Calculator {
    // Overloaded methods
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }

    int add(int a, int b, int c) {
        return a + b + c;
    }
}

public class Main {
    public static void main(String[] args) {
        Calculator calc = new Calculator();
        System.out.println(calc.add(5, 10)); // Calls first method
        System.out.println(calc.add(5.5, 10.5)); // Calls second method
        System.out.println(calc.add(5, 10, 15)); // Calls third method
    }
}
```

---

## 2. Method Overriding
Method overriding allows a subclass to provide a specific implementation of a method that is already defined in its superclass.

### Key Points:
- Happens **between superclass and subclass**.
- Methods must have the **same name, return type, and parameter list**.
- It is an example of **runtime (dynamic) polymorphism**.
- The method in the subclass should be marked with the `@Override` annotation.

### Example:
```java
class Animal {
    void sound() {
        System.out.println("This animal makes a sound.");
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
        Animal myAnimal = new Dog(); // Polymorphism
        myAnimal.sound(); // Calls the overridden method in Dog
    }
}
```

---

## Comparison Table

| Feature               | Method Overloading                          | Method Overriding                          |
|------------------------|---------------------------------------------|--------------------------------------------|
| Definition            | Same method name, different parameter list. | Same method name, same parameter list.     |
| Class Relationship    | Happens within the same class.              | Happens between superclass and subclass.   |
| Polymorphism Type     | Compile-time (static) polymorphism.         | Runtime (dynamic) polymorphism.            |
| Return Type           | Can be different.                          | Must be the same or covariant.             |
| Access Modifier       | No restrictions.                           | Must be the same or more accessible.       |
| Annotation            | Not required.                              | `@Override` annotation is recommended.     |
