# Exception Keywords in Java

Java provides several keywords to handle exceptions effectively. These keywords allow developers to write robust and error-resilient code.

---

## 1. `try`
The `try` block is used to enclose code that might throw an exception. If an exception occurs, it is caught by the corresponding `catch` block.

### Example:
```java
try {
    int result = 10 / 2;
    System.out.println("Result: " + result);
} catch (ArithmeticException e) {
    System.out.println("Exception caught: " + e.getMessage());
} finally {
    System.out.println("This block always executes.");
}
```

## 2. catch
The catch block is used to handle exceptions thrown by the try block. It must immediately follow the try block.

### Example:
```java
try {
    int[] numbers = {1, 2, 3};
    System.out.println(numbers[5]); // May throw ArrayIndexOutOfBoundsException
} catch (ArrayIndexOutOfBoundsException e) {
    System.out.println("Exception caught: " + e.getMessage());
}
```

## 3. finally
The finally block is used to execute code regardless of whether an exception is thrown or not. It is typically used for cleanup operations.

### Example:
```java
try {
    int result = 10 / 2;
    System.out.println("Result: " + result);
} catch (ArithmeticException e) {
    System.out.println("Exception caught: " + e.getMessage());
} finally {
    System.out.println("This block always executes.");
}
```

## 4. throw
The `throw` keyword is used to explicitly throw an exception from a method or any block of code.

### Example:
```java
public class ThrowExample {
    public static void main(String[] args) {
        throw new ArithmeticException("Explicitly thrown exception");
    }
}
```

## 5. throws
The `throws` keyword is used in a method signature to declare that a method can throw one or more exceptions.

### Example:
```java
public class ThrowsExample {
    public static void main(String[] args) throws InterruptedException {
        Thread.sleep(1000); // May throw InterruptedException
    }
}
```



## Summary
| Keyword   | Purpose                                      | Example                                   |
|-----------|----------------------------------------------|-------------------------------------------|
| `try`     | Encloses code that might throw an exception. | `try { int result = 10 / 0; }`            |
| `catch`   | Handles exceptions thrown by the `try` block.| `catch (Exception e) { ... }`             |
| `finally` | Executes code regardless of exception.       | `finally { System.out.println("Cleanup"); }` |
| `throw`   | Explicitly throws an exception.              | `throw new Exception("Error");`           |
| `throws`  | Declares exceptions a method might throw.    | `void method() throws IOException { ... }`|