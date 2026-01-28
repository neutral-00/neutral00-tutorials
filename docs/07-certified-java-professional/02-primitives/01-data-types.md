# Variables and Data Types


## 1. Variables in Java

A **variable** is a named memory location used to store data.

### Syntax

```java
dataType variableName = value;
```

### Example

```java
int age = 25;
String name = "Pritam";
```

### Rules for Variable Names

* Must start with a **letter**, `_`, or `$`
* Cannot start with a number
* Cannot use Java **keywords** (`int`, `class`, `if`, etc.)
* Use **camelCase** by convention

---
Next, let's see what type of data variables can hold in Java.

## 2. Data Types in Java

Java is a **statically typed language**, meaning the type of a variable is known at compile time.

Java data types are divided into **two categories**:

---

## 3. Primitive Data Types

Primitive types store **simple values** directly in memory.

| Type      | Size    | Example              | Description            |
| --------- | ------- | -------------------- | ---------------------- |
| `byte`    | 1 byte  | `byte b = 10;`       | Very small integers    |
| `short`   | 2 bytes | `short s = 100;`     | Small integers         |
| `int`     | 4 bytes | `int n = 5000;`      | Most commonly used     |
| `long`    | 8 bytes | `long l = 100000L;`  | Large integers         |
| `float`   | 4 bytes | `float f = 3.14f;`   | Decimal (less precise) |
| `double`  | 8 bytes | `double d = 3.14;`   | Decimal (default)      |
| `char`    | 2 bytes | `char c = 'A';`      | Single character       |
| `boolean` | 1 bit   | `boolean ok = true;` | True / false           |

### Example

```java
int score = 90;
double price = 99.99;
char grade = 'A';
boolean passed = true;
```

---

## 4. Non-Primitive (aka Reference) Data Types

Non-primitive types store **references to objects**, not the actual value.

Common examples:

### String

```java
String message = "Hello Java";
```

### Array

```java
int[] numbers = {1, 2, 3, 4};
```

### Class / Object

```java
class Student {
    String name;
    int age;
}

Student s = new Student();
```

### Key Differences from Primitive Types

* Can store **multiple values**
* Can be **null**
* Have **methods**

---

## 5. Type Inference (`var`) – Java 10+

Java can infer the type automatically using `var`.

```java
var count = 10;      // int
var text = "Hello"; // String
```

> ⚠️ `var` works only for **local variables**, not fields or parameters.

---

## 6. Type Casting

### Implicit (Widening)

```java
int a = 10;
double b = a; // int → double
```

### Explicit (Narrowing)

```java
double x = 9.8;
int y = (int) x; // 9
```

---

## 7. Summary

* Variables store data in memory
* Java is **strongly and statically typed**
* **Primitive types** store values directly
* **Reference types** store object references
* `var` improves readability (Java 10+)

---

