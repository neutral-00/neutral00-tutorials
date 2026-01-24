# Initialize an Array

## 1. Array Literal (Most Common)

```java
int[] numbers = {1, 2, 3, 4, 5};
```

✔ Clean
✔ Readable
❌ Size is fixed at compile time

---

## 2. Using `new` with Size

```java
int[] numbers = new int[5];
```

Default values:

- `int` → `0`
- `boolean` → `false`
- `Object` → `null`

```java
numbers[0] = 1;
numbers[1] = 2;
```

---

## 3. Using `new` with Values

```java
int[] numbers = new int[]{1, 2, 3, 4, 5};
```

✔ Useful when passing arrays directly to methods

```java
printNumbers(new int[]{1, 2, 3});
```

---

## 4. Using a Loop (Dynamic Initialization)

```java
int[] numbers = new int[5];

for (int i = 0; i < numbers.length; i++) {
    numbers[i] = i + 1;
}
```

✔ When values are calculated

---

## 5. Using `Arrays.fill()`

```java
int[] numbers = new int[5];
Arrays.fill(numbers, 10);
```

Result:

```
[10, 10, 10, 10, 10]
```

---

## 6. Using Streams (Java 8+)

```java
int[] numbers = IntStream.of(1, 2, 3, 4, 5).toArray();
```

Or range-based:

```java
int[] numbers = IntStream.range(1, 6).toArray();
```

✔ Very expressive
✔ Functional style

---

