# OOP Basics

Object Oriented Programming is programming paradigm that uses objects and classes to design applications.

Object Orientation is about simulating the real world in a computer. In real world, we interact with object everyday.

## 1. Classes and Objects

### Class
A class is a blueprint for creating objects. It bundles data and methods into a single unit.

```java
public class Fruit {
    // fields
    String name;
    String color;

    public Fruit(String name, String color){
        this.name = name;
        this.color = color;
    }

    public void displayInfo() {
        System.out.println(this.name + " is "  + this.color + " in color." );
    }
}
```

### Object

An object is an instance of a class. It is a concrete realization of the class.

```java
public class Main {
    public static void main(String[] args) {
        Fruit apple = new Fruit("Apple", "red");
        apple.displayInfo();
    }
}
```
### Constructor

A constructor is a special method that has the same name as the class name. \
It is called when an object is instantiated.

### 4 Pillars of OOP
OOP is based on 4 fundamental concepts also known as 4 pillars which are as follows:

#### 1. Encaptulation

The process of wrapping of fields and methods into a class is called encaptulation. \
Using access specifiers, direct access to the members can be restricted.\

#### 2. Inheritance
Inheritance is a mechanism where a new class, known as subclass, is derived from an existing class, known as superclass. \
The subclass inherits the fields and methods of the superclass.

```java
// Superclass
class Animal {
    public void eat() {
        System.out.println("This animal eats food.");
    }
}

// Subclass
class Dog extends Animal {
    String name;

    public Dog(String name){
        this.name = name;
    }

    public void bark() {
        System.out.println(this.name + " barks woof woof.");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog bruno = new Dog("Bruno");
        bruno.eat();
        bruno.bark();
    }
}
```

#### 3. Polymorphism
Polymorphism allows methods to do different things based on the object it is acting upon. \
There are two types of polymorphism: 
1. compile-time(method overloading) and
2. runtime (method overriding)

```java
// method overloading - compile time polymorphism
public class Calculator {
    public int add(int a , int b) {
        return a + b;
    }

    public double add(double a, double b) {
        return a + b;
    }
}

// method overriding - runtime polymorphism
public class Animal {
    public void makeSound() {
        System.out.println("Generic animal sound");
    }
}

public class Dog extends Animal {
    @Override
    public void makeSound() {
        System.out.println("Dog barks woof woof!");
    }
}
```

#### 4 Abstraction
Abstraction is the concept of hiding the complex implementation details and showing only the essential features of the object. It helps in reducing complexity.

```java
// Abstract class
public abstract class Shape {
    public abstract void draw();
}

// Subclass
public class Circle extends Shape {

    @Override
    public void draw(){
        System.out.println("Drawing a circle");
    }
}

public class Main {
    public static void main(String[] args) {
        Shape c = new Circle();
        c.draw(); // Output: Drawing a circle
    }
}
```

