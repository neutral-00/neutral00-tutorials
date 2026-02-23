# Binary Search - Log n

Why or how binary search is log n?

In computer science,  is called **logarithmic time complexity**. It is often described as the "gold standard" for searching because it stays incredibly fast even as the amount of data grows to millions or billions of items.

### What is logarithm ?

Mathematically, a logarithm is the **inverse of an exponent**. In the context of algorithms like binary search, we almost always use "base 2," written as .

The question a logarithm asks is: **"How many times must I multiply 2 by itself to reach the number ?"** * If , then  (because ).

* If , then  (because ).

---

### How is Binary Search logarithmic time?

Binary search works by **repeatedly halving** the search area. Instead of checking every item one by one (which is ), you look at the middle and throw away half of the remaining items every single time.

To understand why this is , let's look at the "worst-case" scenario: how many steps does it take to reduce a list of size  down to just **1** element?

1. **Step 0:** You have  elements.
2. **Step 1:** You have  elements.
3. **Step 2:** You have  elements (or ).
4. **Step 3:** You have  elements (or ).
5. **Step :** You have  elements.

The search ends when you are down to **1** element. So we solve for :


This means  (the number of steps/iterations) is equal to .

---

### The Power of 

The efficiency of this "halving" approach is massive when  is large. Look at how many steps it takes to find a specific number in a sorted list:

| Items () | Linear Search steps () | Binary Search steps () |
| --- | --- | --- |
| 10 | 10 | ~3-4 |
| 1,000 | 1,000 | ~10 |
| 1,000,000 | 1,000,000 | ~20 |
| 1,000,000,000 | 1,000,000,000 | ~30 |

Even if you have **one billion** items, binary search will find your target in only about 30 comparisons.

[Logarithmic Time Complexity Binary Search](https://www.youtube.com/watch?v=63YxVW5vCL4)
This video provides a great visual breakdown of how the iterations of binary search map to a logarithmic graph.

Let's implement binary search.
```java
public int binarySearch)(int[] nums, int key) {
  int left = 0; 
  int right = nums.length - 1;

  while(left <= right) {
      int mid = left + (right - left) / 2;

      if(key == nums[mid]) {
          return mid;
      } else if(key < nums[mid]) {
          right = mid - 1; // Shrink the upper bound
      } else {
          left = mid + 1;  // Shrink the lower bound
      }
  }

  return -1;
}
```
