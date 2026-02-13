# Control Flow in Java

## 1. What Is Control Flow?

**Control flow** determines **the order in which statements are executed** in a program.

By default, Java executes code **top to bottom**, but control flow statements let us:

* Make decisions
* Repeat actions
* Branch execution

---

## 2. Decision-Making Statements

### 2.1 `if` Statement

Executes code **only if a condition is true**.

```java
int age = 20;

if (age >= 18) {
    System.out.println("Eligible to vote");
}
```

---

### 2.2 `if-else`

```java
int marks = 45;

if (marks >= 50) {
    System.out.println("Pass");
} else {
    System.out.println("Fail");
}
```

---

### 2.3 `if-else-if` Ladder

Used for **multiple conditions**.

```java
int score = 85;

if (score >= 90) {
    System.out.println("Grade A");
} else if (score >= 75) {
    System.out.println("Grade B");
} else {
    System.out.println("Grade C");
}
```

---

### 2.4 `switch` Statement

Best when comparing a **single variable** against multiple values.

```java
int day = 3;

switch (day) {
    case 1 -> System.out.println("Monday");
    case 2 -> System.out.println("Tuesday");
    case 3 -> System.out.println("Wednesday");
    default -> System.out.println("Invalid day");
}
```

> Modern switch syntax (Java 14+) avoids `break`.

---

## 3. Looping Statements

Loops are used to **repeat a block of code**.

---

### 3.1 `for` Loop

Best when the number of iterations is known.

```java
for (int i = 1; i <= 5; i++) {
    System.out.println(i);
}
```

---

### 3.2 `while` Loop

Runs as long as the condition is true.

```java
int i = 1;

while (i <= 5) {
    System.out.println(i);
    i++;
}
```

---

### 3.3 `do-while` Loop

Executes **at least once**, even if the condition is false.

```java
int i = 10;

do {
    System.out.println(i);
} while (i < 5);
```

---

### 3.4 Enhanced `for` Loop (for-each)

Used to iterate over **arrays and collections**.

```java
int[] numbers = {1, 2, 3};

for (int n : numbers) {
    System.out.println(n);
}
```

---

## 4. Branching Statements

### 4.1 `break`

Exits a loop or switch.

```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) {
        break;
    }
}
```

---

### 4.2 `continue`

Skips the current iteration.

```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) {
        continue;
    }
    System.out.println(i);
}
```

---

### 4.3 `return`

Exits a method and optionally returns a value.

```java
int add(int a, int b) {
    return a + b;
}
```

---

## 5. Conditional (Ternary) Operator

Short form of `if-else`.

```java
int age = 16;
String result = (age >= 18) ? "Adult" : "Minor";
```

---

## 6. Exception-Based Control Flow (Brief)

Java can alter flow using exceptions.

```java
try {
    int x = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Cannot divide by zero");
} finally {
    System.out.println("Done");
}
```

---

## 7. Best Practices ⭐

* Prefer `switch` over long `if-else` chains
* Avoid deeply nested conditions
* Use enhanced `for` loops for readability
* Don’t overuse `break` and `continue`

---

## 8. Summary

* `if`, `else`, `switch` → decision making
* `for`, `while`, `do-while` → looping
* `break`, `continue`, `return` → branching
* Ternary operator simplifies conditions

---

