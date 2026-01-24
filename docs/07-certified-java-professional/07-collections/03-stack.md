# Stack

Stack is a data structure that follows Last In First Out.

You can think of like a stack of plates/books.


For code refere `StackExample`

```java

package org.lousing.collections;

import java.util.Stack;

public class StackExample {
    public static void showDemo() {
        // 1. Declare and Initialize
        Stack<String> fruits = new Stack<>();
        // 2. add with push method
        fruits.push("apple");
        fruits.push("banana");
        fruits.push("orange");
        System.out.println(fruits);

        // 3. check which element is current at the top with peek method
        System.out.println("Peek() result : " + fruits.peek());

        // 4. remove the top element at the top with pop method
        System.out.println("Pop() result : " + fruits.pop());

        // 5. peek after pop
        System.out.println("Peek() after popping orange : " + fruits.peek());

    }
}
```
