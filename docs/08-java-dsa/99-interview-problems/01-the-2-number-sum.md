# Find the Two Number Problem

## Problem statement

Given an array of integers, find two numbers that add up to a specific target.

## Project Metadata

- repository: https://github.com/neutral-00/practice-java
- branch: main
- package: org.lousing.algo
- class: TheTwoNumbers

```java
package org.lousing.algo;

/**
 * # Find the Two Numbers Problem
 *
 * ## Problem statement
 *
 * Given an array of integers, find two numbers that add up to a specific target.
 */
public class TheTwoNumbers {
    public static void main(String[] args) {
        int[] numbers = {2, 7, 11, 15};
        int target = 9;

        int[] result = findTwoNumbers(numbers, target);
        if (result != null) {
            System.out.println("Numbers found: " + result[0] + " and " + result[1]);
        } else {
            System.out.println("No two numbers found that add up to the target.");
        }
    }

    public static int[] findTwoNumbers(int[] numbers, int target) {
        java.util.Map<Integer, Integer> numMap = new java.util.HashMap<>();

        for (int number : numbers) {
            int complement = target - number;
            if (numMap.containsKey(complement)) {
                return new int[]{complement, number};
            }
            numMap.put(number, 1);
        }
        return null; // No two numbers found
    }
}

// ## Analyse the time complexity:
// The time complexity of this solution is O(n), where n is the number of elements in the input array.
// This is because we traverse the array only once, and each lookup and insertion in the hash map takes O(1) time on average.

// ## Analyse the space complexity:
// The space complexity is also O(n) in the worst case, as we may need to store all n elements in the hash map
// if no two numbers add up to the target.

```
