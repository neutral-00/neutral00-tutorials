# Exception Types in Java

In Java, exceptions are events that disrupt the normal flow of a program. They are objects that represent an error or unexpected behavior. Java provides a robust mechanism to handle exceptions using the `try-catch` block.

---

## 1. Categories of Exceptions
Java exceptions are broadly categorized into two types:
1. **Checked Exceptions**
2. **Unchecked Exceptions**

---

## 2. Checked Exceptions
Checked exceptions are exceptions that are checked at compile-time. The compiler ensures that these exceptions are either handled using a `try-catch` block or declared using the `throws` keyword.

### Examples:
- `IOException`
- `SQLException`
- `FileNotFoundException`

### Example Code:
```java
import java.io.File;
import java.io.FileReader;

public class CheckedExceptionExample {
    public static void main(String[] args) {
        try {
            File file = new File("nonexistent.txt");
            FileReader fr = new FileReader(file); // May throw FileNotFoundException
        } catch (Exception e) {
            System.out.println("File not found: " + e.getMessage());
        }
    }
}
```

---

## 3. Unchecked Exceptions
Unchecked exceptions are exceptions that are not checked at compile-time. They occur during the execution of the program and are not required to be handled or declared.

### Examples:
- `ArrayIndexOutOfBoundsException`
- `NullPointerException`
- `ArithmeticException`

### Example Code:
```java
public class UncheckedExceptionExample {
    public static void main(String[] args) {
        try {
            int[] numbers = {1, 2, 3};
            System.out.println(numbers[5]); // Throws ArrayIndexOutOfBoundsException
        } catch (Exception e) {
            System.out.println("Exception occurred: " + e.getMessage());
        }
    }
}
```

---

## 4. Errors
Errors are serious problems that a reasonable application should not try to catch. They are usually external to the application and indicate a problem with the environment in which the application is running.

### Examples:
- `StackOverflowError`
- `OutOfMemoryError`

### Example Code:
```java
public class ErrorExample {
    public static void main(String[] args) {
        try {
            recursiveMethod(); // May cause StackOverflowError
        } catch (StackOverflowError e) {
            System.out.println("Stack overflow occurred!");
        }
    }

    public static void recursiveMethod() {
        recursiveMethod(); // Infinite recursion
    }
}
```

## Summary
| Exception Type          | Description                                      | Examples                                   |
|--------------------------|--------------------------------------------------|-------------------------------------------|
| Checked Exceptions       | Checked at compile-time. Must be handled.        | `IOException`, `SQLException`, `FileNotFoundException` |
| Unchecked Exceptions     | Occur at runtime. Usually caused by programming errors. | `NullPointerException`, `ArithmeticException`, `ArrayIndexOutOfBoundsException` |
| Errors                  | Serious issues not meant to be handled by the program. | `OutOfMemoryError`, `StackOverflowError`  |