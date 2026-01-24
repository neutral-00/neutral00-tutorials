# String Comparison



## Why `==` Is Sometimes `true` for Strings in Java

`==` is `true` for Strings when **both references point to the same String object**, usually because of the **String Pool**.


## `==` vs `equals()` (Recap)

### `==`

* Compares **references**
* Same object in memory?

### `equals()`

* Compares **values (characters)**

---

## Case 1: String Literals

```java
String a = "Java";
String b = "Java";

System.out.println(a == b);        // true
System.out.println(a.equals(b));   // true
```

### Why is `==` true?

Java stores **string literals** in a special memory area called the **String Pool**.

* `"Java"` is created **once**
* Both `a` and `b` point to the same pooled object

```
a ──▶ "Java" ◀── b   (String Pool)
```

---

## Case 2: `new String()`

```java
String x = new String("Java");
String y = new String("Java");

System.out.println(x == y);        // false
System.out.println(x.equals(y));   // true
```

### Why is `==` false?

* `new` **forces creation of a new object**
* Each call creates a separate object in the heap

```
x ──▶ "Java"   (Heap)
y ──▶ "Java"   (Heap)
```

Same value, **different objects** → `==` is false

---

## Case 3: Literal vs `new`

```java
String a = "Java";
String b = new String("Java");

System.out.println(a == b);        // false
System.out.println(a.equals(b));   // true
```

### Explanation

* `a` → pooled string
* `b` → heap string

Different memory locations → `==` is false

---

## Case 4: Using `intern()`

```java
String x = new String("Java");
String y = x.intern();

System.out.println(x == y);        // false
System.out.println(y == "Java");   // true
```

### What `intern()` Does

* Checks the **String Pool**
* Returns the pooled instance if it exists
* Otherwise, adds it to the pool

```
"Java" (Pool) ◀── y
"Java" (Heap) ◀── x
```

---

## Case 5: Compile-Time vs Runtime Strings

```java
String a = "Java" + "Script";
String b = "JavaScript";

System.out.println(a == b); // true
```

### Why?

* `"Java" + "Script"` is a **compile-time constant**
* Compiler optimizes it into `"JavaScript"`

---

### Runtime Concatenation

```java
String part = "Java";
String a = part + "Script";
String b = "JavaScript";

System.out.println(a == b); // false
```

* Happens at **runtime**
* Creates a new object

---

## String Pool vs Heap (Big Picture)

```
String Pool (inside Heap)
-------------------------
"Java"
"Hello"

Heap (non-pooled)
-----------------
new String("Java")
```

---

## Why Does Java Do String Pooling?

1. Strings are **heavily used**
2. Strings are **immutable**
3. Saves memory
4. Improves performance

---

## Golden Rules ⭐

1. **Never use `==` to compare Strings**
2. Always use:

   ```java
   a.equals(b)
   ```
3. Use `intern()` only if you understand memory implications
4. String literals are **shared**
5. `new String()` always creates a new object

---

## Interview One-Liner

> `==` may return true for Strings because Java stores string literals in the String Pool and reuses them, but `equals()` should always be used for value comparison.

---

## Summary Table

| Scenario            | `==`  | `equals()` |
| ------------------- | ----- | ---------- |
| Literal vs Literal  | true  | true       |
| new vs new          | false | true       |
| Literal vs new      | false | true       |
| intern() vs literal | true  | true       |

---

Next natural topics (very commonly asked):

* **String immutability (deep dive)**
* **String vs StringBuilder vs StringBuffer**
* **Memory diagram: stack, heap, string pool**
* **Why String is final**

Just tell me where to go next 🚀
