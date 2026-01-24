# Iterate Over Arrays


Assume:

```java
int[] numbers = {1, 2, 3, 4, 5};
```

---

## 1. Traditional `for` Loop (Index-based)

```java
for (int i = 0; i < numbers.length; i++) {
    System.out.println(numbers[i]);
}
```

✔ When you need the index
✔ Can modify elements

---

## 2. Enhanced `for-each` Loop (Most Readable)

```java
for (int num : numbers) {
    System.out.println(num);
}
```

✔ Clean and safe
❌ No index access
❌ Cannot modify array elements directly

---

## 3. While Loop

```java
int i = 0;
while (i < numbers.length) {
    System.out.println(numbers[i]);
    i++;
}
```

✔ Rarely used, but valid

---

## 4. Do-While Loop

```java
int i = 0;
do {
    System.out.println(numbers[i]);
    i++;
} while (i < numbers.length);
```

✔ Executes at least once

---

## 5. Using Streams (Java 8+)

```java
Arrays.stream(numbers).forEach(System.out::println);
```

Or:

```java
IntStream.of(numbers).forEach(n -> System.out.println(n));
```

✔ Functional
✔ Useful for pipelines (filter, map, reduce)

---

## 6. Using `forEach` with Lambda (Java 8+)

```java
Arrays.stream(numbers).forEach(n -> {
    System.out.println(n);
});
```

---

## 7. Reverse Order Loop

```java
for (int i = numbers.length - 1; i >= 0; i--) {
    System.out.println(numbers[i]);
}
```

✔ Common interview pattern

---

# 3️⃣ Modifying Elements While Looping

### Using index-based loop (Correct)

```java
for (int i = 0; i < numbers.length; i++) {
    numbers[i] *= 2;
}
```

### ❌ Using for-each (Won’t work)

```java
for (int n : numbers) {
    n = n * 2; // modifies copy, not array
}
```

---

# 4️⃣ Quick Comparison Table

| Method     | Can Access Index | Can Modify | Readability |
| ---------- | ---------------- | ---------- | ----------- |
| `for`      | ✅               | ✅         | Medium      |
| `for-each` | ❌               | ❌         | High        |
| `while`    | ✅               | ✅         | Low         |
| Stream     | ❌               | ❌         | High        |

---

# 5️⃣ Interview Tip (Very Important)

> **Array size is fixed in Java**
> If size changes → use `List<Integer>` instead.

---
