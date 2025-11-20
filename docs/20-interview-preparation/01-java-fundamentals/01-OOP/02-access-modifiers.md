# Access Modifiers in Java

Access modifiers in Java define the scope and visibility of classes, methods, and variables. They are used to implement encapsulation and control access to the members of a class.

---

## Types of Access Modifiers

| Modifier       | Scope                                                                 | Applicable To                  |
|----------------|----------------------------------------------------------------------|--------------------------------|
| `public`       | Accessible from **anywhere** in the program.                        | Classes, Methods, Variables    |
| `protected`    | Accessible within the **same package** and by **subclasses**.       | Methods, Variables             |
| (default)      | Accessible within the **same package only** (no keyword required).  | Classes, Methods, Variables    |
| `private`      | Accessible only within the **same class**.                          | Methods, Variables             |

| Modifier       | Class | Package | Subclass | World |
|----------------|-------|---------|----------|-------|
| `public`       | ✔     | ✔       | ✔        | ✔     |
| `protected`    | ✔     | ✔       | ✔        | ✘     |
| (default)      | ✔     | ✔       | ✘        | ✘     |
| `private`      | ✔     | ✘       | ✘        | ✘     |

---

## 1. `public`
The `public` modifier allows unrestricted access to the member or class from anywhere in the program.

### Example:
```java
public class PublicExample {
    public String name = "Public Access";

    public void display() {
        System.out.println("This is a public method.");
    }
}
```

## 2. protected
The protected modifier allows access within the same package and to subclasses, even if they are in different packages.

### Example:
```java
class Parent {
    protected void show() {
        System.out.println("This is a protected method.");
    }
}

class Child extends Parent {
    public void display() {
        show(); // Accessible in subclass
    }
}
```

## 3. Default (Package-Private)
If no access modifier is specified, the member or class is accessible only within the same package. This is also known as package-private access.

### Example:
```java
class DefaultExample {
    void display() {
        System.out.println("This is a default access method.");
    }
}
```

## 4. private
The private modifier restricts access to the member within the same class only. It is the most restrictive access level.

### Example:
```java
class PrivateExample {
    private String secret = "Private Access";

    private void displaySecret() {
        System.out.println(secret);
    }

    public void show() {
        displaySecret(); // Accessible within the same class
    }
}
```

Summary

| Modifier       | Class | Package | Subclass | World |
|----------------|-------|---------|----------|-------|
| `public`       | ✔     | ✔       | ✔        | ✔     |
| `protected`    | ✔     | ✔       | ✔        | ✘     |
| (default)      | ✔     | ✔       | ✘        | ✘     |
| `private`      | ✔     | ✘       | ✘        | ✘     |

