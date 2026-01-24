# Space Complexity (Java – DSA)

Space complexity measures how much **memory** an algorithm uses as the input size grows. Like time complexity, it is expressed using **Big-O notation**.

---

## What Space Complexity Includes

Space complexity consists of two parts:

1. **Input Space** – Memory required to store the input data
2. **Auxiliary Space** – Extra memory used by the algorithm (variables, arrays, recursion stack, etc.)

**Total Space Complexity = Input Space + Auxiliary Space**

In most DSA analysis, we focus on **auxiliary space**, since input space is often unavoidable.

---

## O(1) – Constant Space

An algorithm has constant space complexity if it uses a fixed amount of memory regardless of input size.

### Example: Adding Two Numbers

```java
public int sum(int a, int b) {
    return a + b;
}
```

Only a constant number of variables are used, so space complexity is **O(1)**.

---

## O(n) – Linear Space

An algorithm uses linear space if memory usage grows proportionally with input size.

### Example 1: Summing an Array

```java
public int sumArray(int[] array) {
    int sum = 0;
    for (int i = 0; i < array.length; i++) {
        sum += array[i];
    }
    return sum;
}
```

- Input array takes **O(n)** space
- Auxiliary variables (`sum`, `i`) take **O(1)** space

✅ Overall space complexity: **O(n)** (dominated by input size)

---

### Example 2: Creating a New Array

```java
public int[] generate(int n) {
    int[] numbers = new int[n];
    for (int i = 0; i < n; i++) {
        numbers[i] = i;
    }
    return numbers;
}
```

- New array of size `n` is created

✅ Auxiliary space complexity: **O(n)**

---

## Space Complexity in Recursion

Recursive algorithms consume space due to the **call stack**.

### Example: Recursive Fibonacci

```java
int fib(int n) {
    if (n <= 1) return n;
    return fib(n - 1) + fib(n - 2);
}
```

- Maximum recursion depth: `n`
- Each function call takes stack space

✅ Space complexity: **O(n)** (due to recursion stack)

> Note: Even though no extra arrays are used, recursion still consumes memory.

---

## O(log n) – Logarithmic Space

Occurs when recursion depth reduces the problem size by half at each step.

### Example: Binary Search (Recursive)

```java
int binarySearch(int[] arr, int left, int right, int target) {
    if (left > right) return -1;
    int mid = left + (right - left) / 2;
    if (arr[mid] == target) return mid;
    if (arr[mid] > target)
        return binarySearch(arr, left, mid - 1, target);
    return binarySearch(arr, mid + 1, right, target);
}
```

- Recursion depth: **log n**

✅ Space complexity: **O(log n)**

---

## In-Place Algorithms

An algorithm is **in-place** if it uses constant or minimal extra space.

### Example: Reversing an Array

```java
void reverse(int[] arr) {
    int left = 0, right = arr.length - 1;
    while (left < right) {
        int temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;
        left++;
        right--;
    }
}
```

✅ Space complexity: **O(1)**

---

## Summary Table

| Space Complexity | Description                    |
| ---------------- | ------------------------------ |
| O(1)             | Constant extra space           |
| O(log n)         | Recursive calls reducing input |
| O(n)             | Arrays or deep recursion       |
| O(n²)            | 2D arrays                      |

---

## Key Takeaways

- Space complexity measures **memory usage**, not execution time
- Recursion adds hidden space cost via the call stack
- In-place algorithms are memory efficient
- Always consider both **time and space** when designing algorithms

---
