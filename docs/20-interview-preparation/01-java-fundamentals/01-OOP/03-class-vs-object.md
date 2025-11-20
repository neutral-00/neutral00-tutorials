# Class vs Object

Understanding the difference between a **class** and an **object** is fundamental in Object-Oriented Programming (OOP).

---

## 1. What is a Class?
A **class** is a blueprint or template for creating objects. It defines the properties (fields) and behaviors (methods) that the objects created from the class will have.

### Key Points:
- A class is a logical entity.
- It does not occupy memory until an object is created.
- It can contain:
  - Fields (variables)
  - Methods
  - Constructors
  - Nested classes

### Example:
```java
// Defining a class
public class Car {
    String brand;
    int speed;

    void drive() {
        System.out.println("The car is driving.");
    }
}

```

## 2. What is an Object?
An object is an instance of a class. It is a real-world entity that has state (data) and behavior (methods).

### Key Points:
- An object is a physical entity.
- It occupies memory when created.
- It is created using the new keyword.

### Example:
```java
// Creating an object
public class Main {
    public static void main(String[] args) {
        Car myCar = new Car(); // Object creation
        myCar.brand = "Toyota"; // Setting properties
        myCar.speed = 120;

        myCar.drive(); // Calling a method
        System.out.println("Brand: " + myCar.brand);
        System.out.println("Speed: " + myCar.speed);
    }
}
```

