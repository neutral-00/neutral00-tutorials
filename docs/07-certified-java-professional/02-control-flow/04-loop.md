# Looping Statements


## Problem Description

Use for loop to print each digit in a new line entered by user from console.

```java

package org.lousing.andrii.section02;

import java.util.Scanner;

public class LoopExample {

  public static void showDemo() {
    Scanner sc = new Scanner(System.in);
    System.out.print("Please, enter any integer: ");
    String numStr = sc.nextLine().trim(); // trim spaces

    if (numStr.isEmpty()) {
      System.out.println("No input entered!");
    } else {
      for (char ch : numStr.toCharArray()) {
        if (Character.isDigit(ch)) { // optional: only digits
          System.out.println(ch);
        } else {
          System.out.println("'" + ch + "' is not a digit!");
        }
      }
    }

    sc.close();
  }
}
```
