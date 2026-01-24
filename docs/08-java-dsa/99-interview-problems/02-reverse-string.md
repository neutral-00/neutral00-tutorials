# Reverse a String

## Problem statement

Write a function to reverse a string without using built-in functions.

## Project Metadata

- repository: https://github.com/neutral-00/practice-java
- branch: main
- package: org.lousing.algo
- class: StringReverse

```java
package org.lousing.algo;

/**
 * # String Reverse Problem
 * * ## Problem statement
 * * Given a string, reverse it without using any built-in reverse functions.
 */
public class StringReverse {

    public static String reverse(String inputStr) {
        if (inputStr == null) {
            return null;
        }
        StringBuilder result = new StringBuilder();
        for (int i = inputStr.length() - 1; i >= 0; i--) {
            result.append(inputStr.charAt(i));
        }
        return result.toString();
    }

    public static void main(String[] args) {
        String inputStr = "Anderson";
        String reversedStr = reverse(inputStr);
        System.out.println("Input String: " + inputStr);
        System.out.println("Reversed String: " + reversedStr);
        System.out.println("---------------------------");
    }
}

// ## Analyse the time complexity:
// The time complexity of this solution is O(n), where n is the length of the input string.
// This is because we traverse the string once from the end to the beginning, appending each character to the result.

// ## Analyse the space complexity:
// The space complexity is also O(n), as we create a new string to hold the reversed characters.

// Note: if we can use in-built functions, we can simply use new StringBuilder(inputStr).reverse().toString();
```
