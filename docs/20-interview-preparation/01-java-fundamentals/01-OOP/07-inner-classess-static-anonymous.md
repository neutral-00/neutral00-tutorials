# Inner Classes: Static, Non-static, and Anonymous

In Java, an **inner class** is a class defined within another class. Inner classes are used to logically group classes that are only used in one place, and they provide better encapsulation.

---

## 1. Types of Inner Classes
Java supports the following types of inner classes:
1. **Non-static Inner Class (Member Inner Class)**
2. **Static Nested Class**
3. **Anonymous Inner Class**

---

## 2. Non-static Inner Class (Member Inner Class)
A **non-static inner class** is associated with an instance of the outer class. It can access all members (including private members) of the outer class.

### Key Points:
- Requires an instance of the outer class to be instantiated.
- Can access both static and non-static members of the outer class.

### Example:
```java
class Outer {
    private String message = "Hello from Outer class!";

    class Inner {
        void displayMessage() {
            System.out.println(message); // Accessing outer class's private member
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Outer outer = new Outer();
        Outer.Inner inner = outer.new Inner(); // Creating an instance of the inner class
        inner.displayMessage();
    }
}
```

---

## 3. Static Nested Class
A **static nested class** is a static member of the outer class. It can access only the static members of the outer class.

### Key Points:
- Does not require an instance of the outer class to be instantiated.
- Can access only static members of the outer class.

### Example:
```java
class Outer {
    static String staticMessage = "Hello from Outer class!";

    static class StaticNested {
        void displayMessage() {
            System.out.println(staticMessage); // Accessing static member of the outer class
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Outer.StaticNested nested = new Outer.StaticNested(); // Creating an instance of the static nested class
        nested.displayMessage();
    }
}
```

---

## 4. Anonymous Inner Class
An **anonymous inner class** is a class that does not have a name and is defined and instantiated all at once. It is used to override methods of a class or an interface.

### Key Points:
- Does not have a name.
- Defined and instantiated in a single statement.
- Commonly used to override methods of a class or an interface.

### Example:
```java
interface Greeting {
    void sayHello();
}

public class Main {
    public static void main(String[] args) {
        Greeting greeting = new Greeting() { // Anonymous inner class
            @Override
            public void sayHello() {
                System.out.println("Hello from Anonymous Inner Class!");
            }
        };

        greeting.sayHello();
    }
}
```

## 5. Key Differences Between Inner Class Types
| Feature                  | Non-static Inner Class                  | Static Nested Class                     | Anonymous Inner Class                   |
|--------------------------|------------------------------------------|------------------------------------------|------------------------------------------|
| Requires Outer Instance  | Yes                                      | No                                       | No                                       |
| Access to Outer Members  | Can access all members                  | Can access only static members          | Can access all members                  |
| Use Case                 | Grouping logically related classes       | Utility or helper classes                | One-time implementation of interfaces or abstract classes |
