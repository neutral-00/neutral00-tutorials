# Bigdecimal

**NOTES**
- Operations between integers results in integer.
- Operations between integer and double results in double.
- Operations between doubles result in double.
- You will find precision issue when dealing with floating point numbers

---

## Why use BigDecimal over double?
One liner: double has precision issues.

As you noted, floating-point numbers (`double`, `float`) suffer from **precision issues**. This happens because computers represent numbers in binary, and certain decimal fractions (like 0.1) cannot be represented exactly.

```java
// The Precision Issue
double value = 0.02;
double value2 = 0.03;
double result = value2 - value;
System.out.println(result); // Outputs: 0.009999999999999998

```

### 1. Creating BigDecimal Objects

Always prefer the **String constructor**. Using the `double` constructor will actually bring the precision errors into your `BigDecimal`.

* **Recommended:** `new BigDecimal("0.03")`
* **Avoid:** `new BigDecimal(0.03)`

### 2. Basic Operations

Since `BigDecimal` is an object, you cannot use standard operators like `+`, `-`, `*`, or `/`. You must use instance methods:

| Operation | Method | Example |
| --- | --- | --- |
| **Addition** | `.add()` | `a.add(b)` |
| **Subtraction** | `.subtract()` | `a.subtract(b)` |
| **Multiplication** | `.multiply()` | `a.multiply(b)` |
| **Division** | `.divide()` | `a.divide(b, scale, roundingMode)` |

### 3. Handling Division (The "ArithmeticException")

Unlike addition or multiplication, division can result in an infinite decimal (like ). If you don't specify a **scale** (decimal places) and a **rounding mode**, the program will crash.

```java
BigDecimal a = new BigDecimal("1.0");
BigDecimal b = new BigDecimal("3.0");

// This will throw an ArithmeticException:
// BigDecimal c = a.divide(b);

// Correct way:
BigDecimal c = a.divide(b, 2, RoundingMode.HALF_UP); // Result: 0.33

```

### 4. Comparison

Never use `==` or `.equals()` to compare values.

* `.equals()` checks both the **value** and the **scale** (e.g., `1.0` is NOT equal to `1.00`).
* **Use `.compareTo()**` instead. It returns `0` if the values are equal regardless of scale.

```java
BigDecimal x = new BigDecimal("1.0");
BigDecimal y = new BigDecimal("1.00");

System.out.println(x.equals(y));      // false
System.out.println(x.compareTo(y));   // 0 (This means they are equal)

```

---

### 5. Code Example

```java

package org.lousing.andrii.primitives;

import java.math.BigDecimal;
import java.math.RoundingMode;

public class BigDecimalExample {

  public static void showDemo() {
    int totalRideFee = 20;
    int friendsCount = 3;

    System.out.println("20 / 3 is " + totalRideFee / friendsCount);
    System.out.println("(double) 20/3 is " + ((double) totalRideFee / friendsCount));

    BigDecimal rideFee = BigDecimal.valueOf(20).setScale(2);
    BigDecimal noOfPeople = BigDecimal.valueOf(friendsCount);
    BigDecimal chargePerPerson = rideFee.divide(noOfPeople, RoundingMode.HALF_UP);
    System.out.println("chargePerPerson is " + chargePerPerson);

    double d1 = 3.1;
    double d2 = 1.21;

    System.out.println(d1 - d2);

    BigDecimal d3 = BigDecimal.valueOf(d1).setScale(2);
    BigDecimal d4 = BigDecimal.valueOf(d2).setScale(2);
    System.out.println(d3.subtract(d4));
  }
}
```

### Summary Checklist

* [ ] **Always** use Strings in the constructor.
* [ ] **Never** use `==` for comparison; use `compareTo()`.
* [ ] **Always** specify a `RoundingMode` when dividing.
* [ ] **Remember** that `BigDecimal` is immutable (methods return a *new* object).

Would you like me to write a sample code snippet that calculates a store receipt with tax using these principles?
