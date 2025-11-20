# Type Casting in Java

Type casting in Java is the process of converting a variable from one data type to another. It is useful when you need to perform operations between different data types.

---

## 1. Types of Type Casting
Java supports two types of type casting:
1. **Implicit Type Casting (Widening)**: Automatically performed by the compiler.
2. **Explicit Type Casting (Narrowing)**: Must be explicitly performed by the programmer.

---

## 2. Implicit Type Casting (Widening)
Implicit type casting occurs when a smaller data type is automatically converted into a larger data type. This is safe because there is no loss of data.

### Example:
```java
public class ImplicitCastingExample {
    public static void main(String[] args) {
        int num = 100;
        double doubleNum = num; // Implicit casting from int to double

        System.out.println("Integer value: " + num);
        System.out.println("Double value: " + doubleNum);
    }
}
```

---

## 3. Explicit Type Casting (Narrowing)
Explicit type casting occurs when a larger data type is explicitly converted into a smaller data type. This can lead to data loss if the value is too large to fit into the smaller data type.

### Example:
```java
public class ExplicitCastingExample {
    public static void main(String[] args) {
        double doubleNum = 100.99;
        int num = (int) doubleNum; // Explicit casting from double to int

        System.out.println("Double value: " + doubleNum);
        System.out.println("Integer value: " + num); // Fractional part is lost
    }
}
```

---

## 4. Upcasting
Upcasting occurs when a subclass object is assigned to a superclass reference. This is safe because the subclass object can be treated as an instance of the superclass.

### Example:
```java
class Animal {
    void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    void sound() {
        System.out.println("Dog barks");
    }
}

public class UpcastingExample {
    public static void main(String[] args) {
        Animal animal = new Dog(); // Upcasting
        animal.sound(); // Calls the overridden method in Dog
    }
}
```

---

## 5. Downcasting
Downcasting occurs when a superclass reference is cast to a subclass reference. This can be unsafe if the object being cast is not actually an instance of the subclass.

### Example:
```java
public class DowncastingExample {
    public static void main(String[] args) {
        Animal animal = new Dog(); // Upcasting
        Dog dog = (Dog) animal; // Downcasting
        dog.sound(); // Calls the Dog's method
    }
}
```

## Summary
| Type Casting Type       | Description                                      | Example Conversion                       |
|--------------------------|--------------------------------------------------|------------------------------------------|
| Implicit (Widening)      | Automatically converts smaller to larger types. | `int -> double`                          |
| Explicit (Narrowing)     | Manually converts larger to smaller types.      | `double -> int`                          |
| Upcasting                | Converts subclass to superclass reference.      | `Dog -> Animal`                          |
| Downcasting              | Converts superclass reference to subclass.      | `Animal -> Dog`                          |
