# Core Principles of Object-Oriented Programming (OOP)

Object-Oriented Programming (OOP) is a programming paradigm based on the concept of "objects," which can contain data and methods. The four core principles of OOP are:

---

## 1. Encapsulation
Encapsulation is the process of wrapping data (variables) and methods (functions) together into a single unit, typically a class. It restricts direct access to some of the object's components, which is achieved using access modifiers.

### Key Points:
- Protects the internal state of an object.
- Provides controlled access through getters and setters.
- Improves code maintainability and security.

### Example:
```java
public class Person {
    private String name; // Encapsulated field

    // Getter
    public String getName() {
        return name;
    }

    // Setter
    public void setName(String name) {
        this.name = name;
    }
}
```

## 2. Inheritance
Inheritance is a mechanism where a new class inherits properties and behavior (methods) from an existing class. The class that inherits is called the subclass (or derived class), and the class being inherited from is called the superclass (or base class).

### Key Points:
- Promotes code reusability.
- Establishes a natural hierarchy between classes.
- Allows for method overriding.

### Example:
```java
class Animal {
    void eat() {
        System.out.println("This animal eats food.");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("The dog barks.");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.eat(); // Inherited method
        dog.bark(); // Child class method
    }
}
```

## 3. Polymorphism
Polymorphism in Java is a core concept of **object-oriented programming (OOP)** that allows objects to take on many forms. The word "polymorphism" comes from the Greek words **"poly"** (meaning many) and **"morph"** (meaning forms). In simple terms, it means a single action can behave differently based on the object it's performed on. 🎭

There are two main types of polymorphism in Java:

-----

### **Compile-Time Polymorphism (Method Overloading)**

This type of polymorphism is also known as **static polymorphism** because it is resolved during compile time. **Method overloading** is the primary way to achieve this. It involves having multiple methods with the **same name** but **different parameters** (either in the number, type, or order of parameters) within the **same class**. The correct method to be executed is determined by the compiler based on the arguments passed during the method call.

For example:

```java
class Calculator {
    // Method to add two integers
    public int add(int a, int b) {
        return a + b;
    }

    // Overloaded method to add three integers
    public int add(int a, int b, int c) {
        return a + b + c;
    }

    // Another overloaded method to add two doubles
    public double add(double a, double b) {
        return a + b;
    }
}
```

In this example, the `add` method is overloaded. When you call `add(5, 10)`, the compiler knows to use the first method. When you call `add(5.5, 10.5)`, it uses the third.

-----

### **Run-Time Polymorphism (Method Overriding)**

This type of polymorphism is also known as **dynamic polymorphism** because the method call is resolved during run time. **Method overriding** is the key to this concept. It involves a subclass providing a specific implementation for a method that is already defined in its parent class. The method signature (name and parameters) must be **identical** in both the parent and child classes.

A common analogy to understand this is a parent class, say `Animal`, with a method `makeSound()`. Different subclasses like `Dog`, `Cat`, and `Cow` can override this method to provide their own unique sounds.

For example:

```java
class Animal {
    public void makeSound() {
        System.out.println("The animal makes a sound");
    }
}

class Dog extends Animal {
    // Overriding the makeSound method
    @Override
    public void makeSound() {
        System.out.println("The dog barks");
    }
}

class Cat extends Animal {
    // Overriding the makeSound method
    @Override
    public void makeSound() {
        System.out.println("The cat meows");
    }
}
```

When you have a reference of type `Animal` pointing to a `Dog` object, calling `makeSound()` will execute the `Dog`'s version of the method, demonstrating run-time polymorphism.

```java
Animal myPet = new Dog(); // The Animal reference holds a Dog object
myPet.makeSound(); // This will print "The dog barks"
```

## 4. Abstraction
Abstraction is the concept of hiding the complex implementation details and showing only the essential features of the object. It can be achieved using abstract classes and interfaces.

### Key Points:
- Reduces complexity by hiding unnecessary details.
- Promotes code reusability and flexibility.
- Provides a clear separation between the interface and implementation.

### Example:
Abstract Class:

```java
abstract class Shape {
    abstract void draw(); // Abstract method
}

class Circle extends Shape {
    @Override
    void draw() {
        System.out.println("Drawing a circle.");
    }
}
```

Interface:
```java
interface Animal {
    void sound(); // Abstract method
}

class Dog implements Animal {
    @Override
    public void sound() {
        System.out.println("The dog barks.");
    }
}
```

Summary Table

| Principle      | Description                                                     | Example Keywords       |
|----------------|-----------------------------------------------------------------|------------------------|
| Encapsulation  | Wrapping data and methods into a single unit, restricting direct access. | `private`, `get`, `set` |
| Inheritance    | Acquiring properties and methods from a parent class.           | `extends`, `super`     |
| Polymorphism   | Allowing objects to take multiple forms (overloading/overriding). | `@Override`, `overload`|
| Abstraction    | Hiding implementation details, showing only essential features. | `abstract`, `interface`|
