# Read From Console

Code Example

```java

package org.lousing.andrii.primitives;

import java.util.Scanner;

public class ReadFromConsole {

  public static void showDemo() {
    Scanner sc = new Scanner(System.in);
    System.out.println("Enter any word : ");
    String word = sc.next(); // note that input streams block the execution
    System.out.println("You entered : " + word);
    System.out.println("Enter a number: ");
    int n = sc.nextInt();
    System.out.println("You entered : " + n);
    sc.close();
  }
}
```
