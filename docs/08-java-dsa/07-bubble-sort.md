# Bubble sort


### **The Logic: "Sinking" the Heaviest**

Think of the largest numbers as "heavy" bubbles. In each pass through the array, the largest unsorted number "sinks" (or bubbles) to its correct position at the end.

1. **Outer Loop:** Controls how many passes we make. After  passes, the last  elements are already sorted.
2. **Inner Loop:** Compares adjacent pairs ( and ). If the left one is bigger, they swap.
3. **Optimization:** If we go through a whole pass without a single swap, the array is already sorted, and we can stop early.

---

### **Java Implementation**

```java
public static void bubbleSort(int[] arr) {
    int n = arr.length;
    boolean swapped;

    for (int i = 0; i < n - 1; i++) {
        swapped = false;
        
        // Inner loop: n - 1 - i because the last i elements are already in place
        for (int j = 0; j < n - 1 - i; j++) {
            if (arr[j] > arr[j + 1]) {
                // Swap arr[j] and arr[j+1]
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                swapped = true;
            }
        }

        // Optimization: If no two elements were swapped by inner loop, then break
        if (!swapped) break;
    }
}

```

---

### **Performance Breakdown**

| Metric | Complexity | Why? |
| --- | --- | --- |
| **Best Case** |  | Occurs when the array is already sorted (thanks to the `swapped` flag). |
| **Worst Case** |  | Occurs when the array is sorted in reverse order. |
| **Space Complexity** |  | It is an **in-place** algorithm; it doesn't need extra memory. |
| **Stability** | **Stable** | It preserves the relative order of equal elements (it doesn't swap them). |

### **A Pro-Tip for Interviews**

If an interviewer asks why Bubble Sort is rarely used in real-world production (like `Arrays.sort()`), it’s because  grows too fast. For 100,000 items, Bubble Sort might take several minutes, while a more advanced algorithm like **Merge Sort** () would finish in milliseconds.

Would you like me to show you how **Selection Sort** differs, or should we jump to that **Merge Sort** logic I just mentioned?

By the way, to unlock the full functionality of all Apps, enable [Gemini Apps Activity](https://myactivity.google.com/product/gemini).
