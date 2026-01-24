# ArrayDeque

Pronounced as "Array Deck"

It is short for Array Double-Ended Queue. \
It is an array implementation of the `Deque` interface. \
It provides efficient operations for adding/removing/accessing elements from both ends. \


**NOTE**
- It is not thread-safe.
- Thread-safe alternative is `ConcurrentLinkedDeque` from `java.util.concurrent` package.
- ArrayDeque allows null elements.

```java

package org.lousing.collections;

import java.util.ArrayDeque;

public class ArrayDequeExample {
    public static void showDemo() {
        // 1. Declaration and Initialization
        ArrayDeque<String> students = new ArrayDeque();

        // 2. add data
        students.offer("Alice");
        // add at the start
        students.offerFirst("Bob");
        students.offer("Jim");
        // add at the end
        students.offerLast("Charlie");
        System.out.println(students);
        
        // 3. ArrayDeque specific methods
        // ArrayDeque provides efficient operation at the start or end
        System.out.println("PeekFirst() result : " + students.peekFirst());
        System.out.println("PeekLast() result : " + students.peekLast());
        System.out.println("PollFirst() result : " + students.pollFirst());
        System.out.println("PollLast() result : + " + students.pollLast());
        System.out.println(students);
    }
}
```
