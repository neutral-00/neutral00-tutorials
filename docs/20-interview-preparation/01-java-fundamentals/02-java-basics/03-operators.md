# Operators in Java

Operators in Java are special symbols or keywords used to perform operations on variables and values. They are the building blocks of any programming language.

---

## 1. Types of Operators
Java provides the following types of operators:
1. **Arithmetic Operators**
2. **Relational (Comparison) Operators**
3. **Logical Operators**
4. **Bitwise Operators**
5. **Assignment Operators**
6. **Unary Operators**
7. **Ternary Operator**

---

## 2. Arithmetic Operators
Arithmetic operators are used to perform basic mathematical operations.

| Operator | Description       | Example       | Result |
|----------|-------------------|---------------|--------|
| `+`      | Addition          | `5 + 3`       | `8`    |
| `-`      | Subtraction       | `5 - 3`       | `2`    |
| `*`      | Multiplication    | `5 * 3`       | `15`   |
| `/`      | Division          | `5 / 2`       | `2`    |
| `%`      | Modulus (Remainder) | `5 % 2`     | `1`    |

### Example:
```java
public class ArithmeticExample {
    public static void main(String[] args) {
        int a = 10, b = 5;
        System.out.println("Addition: " + (a + b));
        System.out.println("Subtraction: " + (a - b));
        System.out.println("Multiplication: " + (a * b));
        System.out.println("Division: " + (a / b));
        System.out.println("Modulus: " + (a % b));
    }
}
```

---

## 3. Relational (Comparison) Operators
Relational operators are used to compare two values. They return a boolean result (`true` or `false`).

| Operator | Description       | Example       | Result  |
|----------|-------------------|---------------|---------|
| `==`     | Equal to          | `5 == 3`      | `false` |
| `!=`     | Not equal to      | `5 != 3`      | `true`  |
| `>`      | Greater than      | `5 > 3`       | `true`  |
| `<`      | Less than         | `5 < 3`       | `false` |
| `>=`     | Greater than or equal to | `5 >= 3` | `true`  |
| `<=`     | Less than or equal to | `5 <= 3`   | `false` |

### Example:
```java
public class RelationalExample {
    public static void main(String[] args) {
        int a = 5, b = 3;
        System.out.println("a == b: " + (a == b)); // false
        System.out.println("a != b: " + (a != b)); // true
        System.out.println("a > b: " + (a > b));   // true
        System.out.println("a < b: " + (a < b));   // false
        System.out.println("a >= b: " + (a >= b)); // true
        System.out.println("a <= b: " + (a <= b)); // false
    }
}
```
---

## 4. Logical Operators
Logical operators are used to combine multiple conditions and return a boolean result (`true` or `false`).

| Operator | Description       | Example               | Result  |
|----------|-------------------|-----------------------|---------|
| `&&`     | Logical AND       | `(5 > 3) && (5 > 2)`  | `true`  |
| `\|\|`     | Logical OR        | `(5 > 3) \|\| (5 < 2)`  | `true`  |
| `!`      | Logical NOT       | `!(5 > 3)`            | `false` |

### Example:
```java
public class LogicalExample {
    public static void main(String[] args) {
        int a = 5, b = 3, c = 2;

        // Logical AND
        System.out.println("(a > b) && (a > c): " + ((a > b) && (a > c))); // true

        // Logical OR
        System.out.println("(a > b) || (a < c): " + ((a > b) || (a < c))); // true

        // Logical NOT
        System.out.println("!(a > b): " + (!(a > b))); // false
    }
}
```

## 5. Bitwise Operators
Bitwise operators are used to perform operations on individual bits of integer values.

| Operator | Description       | Example       | Result |
|----------|-------------------|---------------|--------|
| `&`      | Bitwise AND       | `5 & 3`       | `1`    |
| `\|`      | Bitwise OR        | `5 \| 3`       | `7`    |
| `^`      | Bitwise XOR       | `5 ^ 3`       | `6`    |
| `<<`     | Left Shift        | `5 << 1`      | `10`   |
| `>>`     | Right Shift       | `5 >> 1`      | `2`    |

### Example:
```java
public class BitwiseExample {
    public static void main(String[] args) {
        int a = 5, b = 3;
        System.out.println("Bitwise AND: " + (a & b));
        System.out.println("Bitwise OR: " + (a | b));
        System.out.println("Bitwise XOR: " + (a ^ b));
        System.out.println("Left Shift: " + (a << 1));
        System.out.println("Right Shift: " + (a >> 1));
    }
}
```

---

## 6. Unary Operators
Unary operators are used to perform operations on a single operand.

| Operator | Description       | Example       | Result |
|----------|-------------------|---------------|--------|
| `+`      | Unary Plus        | `+5`          | `5`    |
| `-`      | Unary Minus       | `-5`          | `-5`   |
| `++`     | Pre-Increment     | `++a`         | `6`    |
| `++`     | Post-Increment    | `a++`         | `5`    |
| `!`      | Logical NOT       | `!true`       | `false`|

### Example:
```java
public class UnaryExample {
    public static void main(String[] args) {
        int a = 5;
        System.out.println("Unary Plus: " + (+a));
        System.out.println("Unary Minus: " + (-a));
        System.out.println("Pre-Increment: " + (++a));
        System.out.println("Post-Increment: " + (a++));
        System.out.println("After Post-Increment: " + a);
        System.out.println("Logical NOT: " + (!true));
    }
}
```

---

## 7. Ternary Operator
The ternary operator is a shorthand for the `if-else` statement. It takes three operands and returns a value based on the condition.

### Syntax:
```java
condition ? value_if_true : value_if_false;
```

### Example:
```java
public class TernaryExample {
    public static void main(String[] args) {
        int a = 5, b = 3;
        String result = (a > b) ? "a is greater" : "b is greater";
        System.out.println(result);
    }
}
```
