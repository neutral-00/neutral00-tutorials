# String

## Syllabus
- `String` overview
- Methods
- String creation
- String pool
- String comparison
- Escape sequences
- String formatting
- Regular Expressions


---

## 1. `String` overview

* `String` represents a **sequence of characters**
* It is **immutable** (cannot be changed after creation)
* Part of `java.lang`, so no import needed

```java
String s = "Hello";
```

Any “modification” creates a **new String object**.

---

## 2. Common `String` methods

Some frequently used ones:

```java
String s = "  Java Strings  ";

s.length();              // number of characters
s.charAt(2);             // character at index
s.substring(2, 6);       // part of string
s.toUpperCase();         // convert case
s.toLowerCase();
s.trim();                // remove leading/trailing ASCII spaces
s.strip();               // remove Unicode whitespace (Java 11+)
s.replace("a", "o");     // replace text
s.contains("Java");      // check presence
s.startsWith("Java");
s.endsWith("ings");
```

---

## 3. String creation

Two main ways:

```java
String s1 = "Java";              // string literal
String s2 = new String("Java");  // new object
```

* Literal form is **preferred**
* `new String()` always creates a new object

---

## 4. String pool

* Java stores string literals in a **String Pool**
* Identical literals point to the **same object**

```java
String a = "Java";
String b = "Java";

a == b;        // true (same reference)
```

But:

```java
String c = new String("Java");

a == c;        // false
```

The pool saves memory and improves performance.

---

## 5. String comparison

### ❌ Don’t use `==` for content

```java
s1 == s2;   // compares references
```

### ✅ Use `.equals()`

```java
s1.equals(s2);  // compares content
```

### Case-insensitive comparison

```java
s1.equalsIgnoreCase(s2);
```

---

## 6. Escape sequences

Used inside string literals to represent special characters:

| Escape | Meaning         |
| ------ | --------------- |
| `\"`   | double quote    |
| `\\`   | backslash       |
| `\n`   | new line        |
| `\t`   | tab             |
| `\r`   | carriage return |

```java
System.out.println("Hello\nWorld");
System.out.println("Path: C:\\Java\\bin");
```

---

## 7. String formatting

### Using `String.format()`

```java
String name = "Alice";
int age = 25;

String result = String.format("Name: %s, Age: %d", name, age);
```

### Using `printf()`

```java
System.out.printf("Name: %s, Age: %d%n", name, age);
```

Common format specifiers:

* `%s` → String
* `%d` → integer
* `%f` → floating point
* `%.2f` → 2 decimal places

---

## 8. Regular Expressions (Regex)

Regex is used for **pattern matching** in strings.

### Simple examples

```java
String s = "abc123";

s.matches("[a-z]+\\d+");  // true
```

### Using `replaceAll()`

```java
String text = "Java123";

text.replaceAll("\\d", "");  // "Java"
```

### Common regex patterns

| Pattern | Meaning        |
| ------- | -------------- |
| `.`     | any character  |
| `\\d`   | digit          |
| `\\w`   | word character |
| `+`     | one or more    |
| `*`     | zero or more   |

⚠️ Regex uses **double escaping** inside Java strings.

---

## Key takeaways

* `String` is immutable
* Prefer string literals over `new String()`
* Always use `.equals()` for comparison
* Use `strip()` over `trim()` when possible
* Regex is powerful but needs careful escaping

