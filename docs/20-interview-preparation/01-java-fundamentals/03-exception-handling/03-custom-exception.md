# Custom Exceptions in Java

In Java, you can create your own exceptions by extending the `Exception` class or the `RuntimeException` class. Custom exceptions are useful when you want to handle specific application-related errors.

---

## 1. Steps to Create a Custom Exception
1. Create a class that extends `Exception` (for checked exceptions) or `RuntimeException` (for unchecked exceptions).
2. Provide constructors to initialize the exception object.
3. Optionally, override the `toString()` or `getMessage()` method to provide a custom error message.

---

## 2. Example of a Custom Checked Exception
A custom checked exception must extend the `Exception` class.

### Example:
```java
// Custom checked exception
class InvalidAgeException extends Exception {
    public InvalidAgeException(String message) {
        super(message);
    }
}

public class CustomCheckedExceptionExample {
    public static void main(String[] args) {
        try {
            validateAge(15); // Throws InvalidAgeException
        } catch (InvalidAgeException e) {
            System.out.println("Exception caught: " + e.getMessage());
        }
    }

    public static void validateAge(int age) throws InvalidAgeException {
        if (age < 18) {
            throw new InvalidAgeException("Age must be 18 or above.");
        }
    }
}
```

---

## 3. Example of a Custom Unchecked Exception
A custom unchecked exception must extend the `RuntimeException` class.

### Example:
```java
// Custom unchecked exception
class InvalidInputException extends RuntimeException {
    public InvalidInputException(String message) {
        super(message);
    }
}

public class CustomUncheckedExceptionExample {
    public static void main(String[] args) {
        validateInput(-5); // Throws InvalidInputException
    }

    public static void validateInput(int number) {
        if (number < 0) {
            throw new InvalidInputException("Input must be a positive number.");
        }
    }
}
```

## Key Differences Between Checked and Unchecked Custom Exceptions
| Feature                  | Checked Custom Exception                  | Unchecked Custom Exception               |
|--------------------------|-------------------------------------------|------------------------------------------|
| Base Class               | Extends `Exception`.                     | Extends `RuntimeException`.              |
| Compile-Time Check       | Checked by the compiler.                 | Not checked by the compiler.             |
| Handling Requirement     | Must be handled using `try-catch` or declared with `throws`. | Optional to handle.                      |
| Use Case                 | Used for recoverable errors.             | Used for programming errors.             |

