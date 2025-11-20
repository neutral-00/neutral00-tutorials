# String Handling in Java

In Java, strings are objects that represent a sequence of characters. The `String` class in Java provides various methods to manipulate and work with strings.

---

## 1. Characteristics of Strings in Java
- Strings are **immutable**: Once created, their values cannot be changed.
- The `String` class is part of the `java.lang` package.
- Strings can be created using:
  1. **String Literals**
  2. **`new` Keyword**

### Example:
```java
public class StringExample {
    public static void main(String[] args) {
        // Using String literal
        String str1 = "Hello";

        // Using new keyword
        String str2 = new String("World");

        System.out.println(str1 + " " + str2); // Output: Hello World
    }
}
```

## 2. String Comparison in Java
Strings in Java can be compared using the `equals()` method, the `==` operator, and the `compareTo()` method.

### Example:
```java
public class StringComparison {
    public static void main(String[] args) {
        String str1 = "Hello";
        String str2 = "Hello";
        String str3 = new String("Hello");

        // Using equals()
        System.out.println(str1.equals(str2)); // true
        System.out.println(str1.equals(str3)); // true

        // Using ==
        System.out.println(str1 == str2); // true (same reference)
        System.out.println(str1 == str3); // false (different reference)

        // Using compareTo()
        System.out.println(str1.compareTo(str2)); // 0 (equal)
        System.out.println(str1.compareTo("World")); // Negative value
    }
}
```

## 3. StringBuilder in Java
The `StringBuilder` class is used to create mutable (modifiable) string objects. It is more efficient than `String` when performing multiple string manipulations.

### Example:
```java
public class StringBuilderExample {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder("Hello");
        sb.append(" World");
        System.out.println(sb); // Output: Hello World
    }
}
```

## Common String Methods
| Method                  | Description                                      | Example                                   |
|-------------------------|--------------------------------------------------|-------------------------------------------|
| `length()`              | Returns the length of the string.               | `"Hello".length()` → `5`                  |
| `charAt(index)`         | Returns the character at the specified index.   | `"Hello".charAt(1)` → `e`                 |
| `substring(start, end)` | Returns a substring from start to end index.    | `"Hello".substring(1, 4)` → `ell`         |
| `contains()`            | Checks if the string contains a sequence.       | `"Hello".contains("ll")` → `true`         |
| `equals()`              | Compares two strings for equality.              | `"Hello".equals("hello")` → `false`       |
| `equalsIgnoreCase()`    | Compares two strings, ignoring case.            | `"Hello".equalsIgnoreCase("hello")` → `true` |
| `toUpperCase()`         | Converts the string to uppercase.               | `"Hello".toUpperCase()` → `HELLO`         |
| `toLowerCase()`         | Converts the string to lowercase.               | `"Hello".toLowerCase()` → `hello`         |
| `trim()`                | Removes leading and trailing spaces.            | `" Hello ".trim()` → `"Hello"`            |
| `replace(old, new)`     | Replaces occurrences of a character or string.  | `"Hello".replace("l", "p")` → `Heppo`     |


## StringBuilder vs StringBuffer
| Feature           | StringBuilder                          | StringBuffer                           |
|--------------------|----------------------------------------|----------------------------------------|
| Mutability         | Mutable (modifiable).                 | Mutable (modifiable).                  |
| Thread-Safety      | Not thread-safe (not synchronized).   | Thread-safe (synchronized).            |
| Performance        | Faster due to no synchronization.     | Slower due to synchronization overhead.|
| Use Case           | Suitable for single-threaded programs.| Suitable for multi-threaded programs.  |

### Example of StringBuilder:
```java
public class StringBuilderExample {
    public static void main(String[] args) {
        StringBuilder sb = new StringBuilder("Hello");
        sb.append(" World");
        System.out.println(sb); // Output: Hello World
    }
}
```

### Example of StringBuffer:
```java
public class StringBufferExample {
    public static void main(String[] args) {
        StringBuffer sb = new StringBuffer("Hello");
        sb.append(" World");
        System.out.println(sb); // Output: Hello World
    }
}
```
