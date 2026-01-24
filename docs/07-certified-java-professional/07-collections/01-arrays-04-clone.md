# Clone Array

In Java, every array is an object, and all arrays inherit from `Object`. This means they come with a built-in `clone()` method. When you clone an array, you are creating a copy of the array itself.

However, there is a very important distinction to understand: **Shallow Copy vs. Deep Copy.**

---

### How it Works

When you call `.clone()` on a Java array:

1. **For Primitives (`int`, `double`, etc.):** It creates a completely independent copy of the values. Changing the copy won't affect the original.
2. **For Objects (`String`, `CustomObject`):** It creates a **shallow copy**. It copies the *references* to the objects, not the objects themselves. Both arrays will point to the same objects in memory.

---

### 1. Cloning Primitive Arrays (Deep Copy behavior)

Since primitives hold actual values, cloning them effectively creates a deep copy.

```java
int[] original = {1, 2, 3};
int[] copy = original.clone();

copy[0] = 99; // Change the copy

System.out.println(original[0]); // Output: 1 (Original is safe!)
System.out.println(copy[0]);     // Output: 99

```

### 2. Cloning Object Arrays (Shallow Copy behavior)

For arrays of objects, the behavior is different. The "buckets" are copied, but they still point to the same "items."

```java
StringBuilder[] original = { new StringBuilder("A"), new StringBuilder("B") };
StringBuilder[] copy = original.clone();

// Modifying an object INSIDE the cloned array
copy[0].append("pplied"); 

System.out.println(original[0]); // Output: Applied (Original was changed!)

```

---

### Key Advantages of `array.clone()`

* **Performance:** It is generally the fastest way to copy an array because it uses an optimized native method.
* **Type Safety:** Unlike `Object.clone()`, which returns an `Object` that you must cast, `array.clone()` automatically returns the correct array type (e.g., `int[]` returns `int[]`).

---

### Comparison with other methods

| Method | Best Use Case |
| --- | --- |
| **`array.clone()`** | Quickest and easiest way for 1D arrays. |
| **`System.arraycopy()`** | Best for partial copies (copying a specific range). |
| **`Arrays.copyOf()`** | Best for resizing an array while copying. |

---

### A Warning on Multidimensional Arrays

If you clone a 2D array (e.g., `int[][]`), only the "outer" array is cloned. The "inner" arrays are still shared between the original and the copy. This is a common source of bugs in Java!

Would you like to see how to properly perform a **Deep Copy** of a 2D array or an object array so they are truly independent?
