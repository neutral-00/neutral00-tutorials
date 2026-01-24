# Wrapper Classes in Java

## 1. What Are Wrapper Classes?

**Wrapper classes** are object representations of Java’s **primitive data types**.

> They “wrap” primitive values inside objects.

### Why they exist?

* Java is **object-oriented**
* Some features work **only with objects**, not primitives

---

## 2. Primitive Types vs Wrapper Classes

| Primitive | Wrapper Class |
| --------- | ------------- |
| `byte`    | `Byte`        |
| `short`   | `Short`       |
| `int`     | `Integer`     |
| `long`    | `Long`        |
| `float`   | `Float`       |
| `double`  | `Double`      |
| `char`    | `Character`   |
| `boolean` | `Boolean`     |

---

## 3. Why Do We Need Wrapper Classes?

### 1️⃣ Collections Framework

Collections can store **objects only**.

❌ Not allowed:

```java
List<int> numbers;
```

✅ Allowed:

```java
List<Integer> numbers = new ArrayList<>();
numbers.add(10);
```

---

### 2️⃣ Utility Methods

Wrapper classes provide useful methods.

```java
int num = Integer.parseInt("123");
String s = Integer.toString(100);
```

---

### 3️⃣ Null Handling

Primitives cannot be `null`, wrapper objects can.

```java
Integer count = null; // valid
int total = null;     // ❌ compile-time error
```

Useful in:

* Databases
* APIs
* Optional values

---

## 4. Creating Wrapper Objects

### ❌ Old Style (Deprecated)

```java
Integer a = new Integer(10); // deprecated
```

### ✅ Recommended Ways

#### Using `valueOf()`

```java
Integer a = Integer.valueOf(10);
```

#### Using Autoboxing (Most Common)

```java
Integer b = 20; // int → Integer
```

---

## 5. Autoboxing and Unboxing

### Autoboxing

Primitive → Wrapper

```java
int x = 5;
Integer y = x;
```

### Unboxing

Wrapper → Primitive

```java
Integer a = 10;
int b = a;
```

> Introduced in **Java 5**

---

## 6. Wrapper Classes Are Immutable

Once created, their value **cannot be changed**.

```java
Integer a = 10;
a = 20; // new object created
```

Same applies to:

* `String`
* All wrapper classes

---

## 7. Comparison: `==` vs `equals()`

### ❌ Using `==` (checks reference)

```java
Integer x = 200;
Integer y = 200;

System.out.println(x == y); // false
```

### ✅ Using `equals()` (checks value)

```java
System.out.println(x.equals(y)); // true
```

### Integer Caching

* Java caches values from **-128 to 127**
* `==` may behave unexpectedly

👉 **Always use `equals()` for wrappers**

---

## 8. Common Utility Methods

```java
Integer.max(10, 20);      // 20
Integer.min(10, 20);      // 10
Integer.sum(10, 20);      // 30

Double.parseDouble("3.14");
Boolean.parseBoolean("true");
```

---

## 9. When to Use Primitive vs Wrapper

| Use Case                  | Prefer    |
| ------------------------- | --------- |
| Performance-critical code | Primitive |
| Collections               | Wrapper   |
| Nullable values           | Wrapper   |
| Database / ORM            | Wrapper   |
| Simple calculations       | Primitive |

---

## 10. Interview Tip ⭐

**Question:** Why doesn’t Java use wrapper classes everywhere?

**Answer:**
Wrapper classes:

* Consume more memory
* Are slower due to object creation
* Need boxing/unboxing

So Java keeps primitives for **performance**.

---

## 11. Summary

* Wrapper classes convert primitives into objects
* Required for collections and object-based APIs
* Support autoboxing and unboxing
* Are immutable
* Use `equals()`, not `==`

---

