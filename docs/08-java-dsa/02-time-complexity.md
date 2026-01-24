# Time Complexity (Java – DSA)

Time complexity describes how the running time of an algorithm grows as the input size grows. In Data Structures & Algorithms (DSA), we use **Big-O notation** to express this growth.

---

## O(1) – Constant Time

An algorithm runs in constant time if its execution time does not depend on the input size.

**Example:** Accessing an array element or a HashMap value by key.

```java
int[] arr = {1, 2, 3, 4};
System.out.println(arr[2]); // O(1)
```

---

## O(n) – Linear Time

If the running time increases linearly with the input size, the algorithm has O(n) time complexity.

**Example:** Traversing an array.

```java
for (int i = 0; i < arr.length; i++) {
    System.out.println(arr[i]);
}
```

If the input size doubles, the number of operations also roughly doubles.

---

## O(log n) – Logarithmic Time

An algorithm has logarithmic time complexity when the input size is reduced by a constant factor (usually half) in each step.

**Example:** Binary Search (on a sorted array).

```java
int binarySearch(int[] arr, int target) {
    int left = 0, right = arr.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (arr[mid] == target) return mid;
        if (arr[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
```

---

## O(n²) – Quadratic Time

Quadratic time complexity usually occurs when there are **nested loops**.

**Example:** Comparing every element with every other element.

```java
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        System.out.println(i + ", " + j);
    }
}
```

If input size doubles, operations increase roughly four times.

---

## O(n³) – Cubic Time

Occurs when there are **three nested loops**.

```java
for (int i = 0; i < n; i++) {
    for (int j = 0; j < n; j++) {
        for (int k = 0; k < n; k++) {
            System.out.println(i + ", " + j + ", " + k);
        }
    }
}
```

This becomes impractical very quickly as input size grows.

---

## O(2ⁿ) – Exponential Time

In exponential time complexity, each additional input element doubles the number of operations.

**Example:** Recursive Fibonacci (inefficient version).

```java
int fib(int n) {
    if (n <= 1) return n;
    return fib(n - 1) + fib(n - 2);
}
```

Used mainly for explanation purposes; should be avoided in real applications.

---

## O(n!) – Factorial Time

Factorial time complexity occurs in problems that generate **all permutations** of a set.

**Example:** Generating permutations.

```java
void permute(String str, String result) {
    if (str.length() == 0) {
        System.out.println(result);
        return;
    }
    for (int i = 0; i < str.length(); i++) {
        permute(str.substring(0, i) + str.substring(i + 1),
                result + str.charAt(i));
    }
}
```

This complexity grows extremely fast and is only feasible for very small inputs.

---

## Summary Table

| Complexity | Name        | Example             |
| ---------- | ----------- | ------------------- |
| O(1)       | Constant    | Array access        |
| O(log n)   | Logarithmic | Binary search       |
| O(n)       | Linear      | Array traversal     |
| O(n²)      | Quadratic   | Nested loops        |
| O(n³)      | Cubic       | Triple nested loops |
| O(2ⁿ)      | Exponential | Recursive Fibonacci |
| O(n!)      | Factorial   | Permutations        |

---

## Key Takeaways

- Always aim for **O(1), O(log n), or O(n)** solutions when possible
- Avoid **O(2ⁿ)** and **O(n!)** except for very small inputs
- Time complexity helps compare algorithms, not exact execution time

---

Next topics you can study:

- Space Complexity
- Recursion vs Iteration
- Arrays & Strings (DSA in Java)
- Sorting Algorithms (Bubble, Selection, Merge, Quick)
