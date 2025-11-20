# Data Types in Java

In Java, data types specify the size and type of values that can be stored in variables. Java is a statically-typed language, meaning every variable must be declared with a data type.

---

## 1. Types of Data Types
Java data types are broadly categorized into two types:
1. **Primitive Data Types**
2. **Non-Primitive (Reference) Data Types**

---

## 2. Primitive Data Types
Primitive data types are the most basic data types in Java. They are predefined by the language and represent simple values.

### Categories of Primitive Data Types:
| Data Type   | Size       | Default Value | Description                          |
|-------------|------------|---------------|--------------------------------------|
| `byte`      | 1 byte     | 0             | Stores whole numbers from -128 to 127. |
| `short`     | 2 bytes    | 0             | Stores whole numbers from -32,768 to 32,767. |
| `int`       | 4 bytes    | 0             | Stores whole numbers from -2^31 to 2^31-1. |
| `long`      | 8 bytes    | 0L            | Stores whole numbers from -2^63 to 2^63-1. |
| `float`     | 4 bytes    | 0.0f          | Stores fractional numbers, up to 7 decimal digits. |
| `double`    | 8 bytes    | 0.0d          | Stores fractional numbers, up to 15 decimal digits. |
| `char`      | 2 bytes    | '\u0000'      | Stores a single 16-bit Unicode character. |
| `boolean`   | 1 bit      | `false`       | Stores `true` or `false`.            |

### Example:
```java
public class DataTypesExample {
    public static void main(String[] args) {
        int age = 25; // Integer type
        double salary = 55000.50; // Double type
        char grade = 'A'; // Character type
        boolean isEmployed = true; // Boolean type

        System.out.println("Age: " + age);
        System.out.println("Salary: " + salary);
        System.out.println("Grade: " + grade);
        System.out.println("Employed: " + isEmployed);
    }
}
```

---

## 3. Non-Primitive (Reference) Data Types
Non-primitive data types are created by the programmer and are not defined by Java (except for `String`). They can be used to call methods to perform certain operations, while primitive types cannot.

### Example:
```java
public class ReferenceTypesExample {
    public static void main(String[] args) {
        String name = "John Doe"; // String type
        int[] numbers = {1, 2, 3, 4, 5}; // Array type

        System.out.println("Name: " + name);
        System.out.println("First number: " + numbers[0]);
    }
}
```

### Comparison of Primitive and Non-Primitive Data Types:
| Feature                  | Primitive Data Types                     | Non-Primitive Data Types                |
|--------------------------|-------------------------------------------|------------------------------------------|
| Definition               | Predefined by the language.              | Created by the programmer.               |
| Memory Usage             | Stores actual values.                    | Stores references to objects.            |
| Methods                  | Cannot call methods on primitive types.  | Can call methods on non-primitive types. |
| Default Value            | Depends on the type (e.g., 0, false).    | `null`.                                  |