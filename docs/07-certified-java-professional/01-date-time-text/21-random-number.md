# Random Number - Generation

## Problem Description

Write a program to simulate rolling a dice. You should get a random number between 1 and 6.

```java
// program to get a random number between 1-6
import java.util.Random;

public class RandomNumber {

  public static void showDemo() {
    // let's simulate rolling a dice.
    Random r = new Random();
    System.out.println(r.nextInt(6) + 1);
  }
}
```
