# Arrays (Java – DSA)

Video time line: https://youtu.be/xwI5OBEnsZU?t=3075

- An **array** is a linear data structure used to store multiple values of the **same data type** in a single variable. 
- The elements are stored in **contiguous memory locations** and are accessed using an **index**.

---

## Characteristics of Arrays

- Stores elements of the **same data type**
- Uses **contiguous memory allocation**
- Has a **fixed size** once created
- Elements are accessed using **zero-based indexing**
- Provides **fast random access**

## Limitaion
- Fixed size
---

## Array Declaration and Initialization (Java)

### Declaration

```java
int[] arr;
```

### Allocation

```java
arr = new int[5];
```

### Declaration + Initialization

```java
int[] arr = {10, 20, 30, 40, 50};
```

---

## Accessing Array Elements

```java
int[] arr = {10, 20, 30};
System.out.println(arr[0]); // 10
System.out.println(arr[2]); // 30
```

Accessing an element using an index takes **O(1)** time.

---

## Traversing an Array

### Using for loop

```java
for (int i = 0; i < arr.length; i++) {
    System.out.println(arr[i]);
}
```

### Using enhanced for loop

```java
for (int num : arr) {
    System.out.println(num);
}
```

---

## Common Array Operations

### 1. Insertion

- At end: O(1)
- At beginning or middle: O(n) (elements must be shifted)

### 2. Deletion

- From end: O(1)
- From beginning or middle: O(n)

### 3. Searching

- Linear Search: O(n)
- Binary Search (sorted array): O(log n)

### 4. Update

- Update by index: O(1)

---

## Time Complexity of different array operations Summary

| Operation | Time Complexity |
| --------- | --------------- |
| Access    | O(1)            |
| Insert    | O(n)            |
| Traverse  | O(n)            |
| Search    | O(n)            |
| Delete    | O(n)            |
| Update    | O(1)            |

---

## Space Complexity

- Arrays use **O(n)** space
- No extra auxiliary space for traversal → **O(1)**

---

## Advantages of Arrays

- Fast access using index
- Simple and easy to use
- Efficient memory usage (no overhead per element)
- Cache friendly
- Ease of sorting
- Implement other data structures

---

## Disadvantages of Arrays

- Fixed size (cannot grow dynamically)
- Insertion and deletion are costly
- Possible memory wastage

---

## Use case
1. Implement other data structure
1. Caching
1. Graphs - visited nodes
1. Mathematical computations
1. Common Coding


## Types of Arrays in Java

### 1. One-Dimensional Array

```java
int[] arr = new int[5];
```

### 2. Two-Dimensional Array

```java
int[][] matrix = new int[3][3];
```

---

## Example: Sum of Array Elements

```java
public int sumArray(int[] arr) {
    int sum = 0;
    for (int num : arr) {
        sum += num;
    }
    return sum;
}
```

---

## Key Takeaways

- Arrays are the foundation of many data structures
- Best suited for scenarios with fixed-size data
- Excellent for index-based access

---

### Next Topics

- Array Problems (Reverse, Max/Min, Rotation)
- Two-Pointer Technique
- Sliding Window Technique
