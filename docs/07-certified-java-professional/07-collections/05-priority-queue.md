# Priority Queue

It is a special data structure that orders elements based on their natural ordering or a specialized comparator.

It is implemented as a heap. \
It allows efficient retrieval of the highest/lowest priority element.

```java

package org.lousing.collections;

import java.util.Comparator;
import java.util.PriorityQueue;
import java.util.Queue;

public class PriorityQueueExample {

    public static void showDemo() {
        System.out.println("--PriorityQueue with default MIN heap logic--");
        //1. Declaration and Initialization
        Queue<String> trainTicketQueue = new PriorityQueue<>();


        // 2. add data
        trainTicketQueue.offer("Jim");
        trainTicketQueue.offer("Jany");
        trainTicketQueue.offer("Alice");
        // by default there is a min heap implementation
        // so priority is given base on alphabetical order
        System.out.println(trainTicketQueue);
        // So Right now Alice got the highest priority
        System.out.println("Peek() result: " + trainTicketQueue.peek());

        // 3. remove data
        System.out.println("Poll result : " + trainTicketQueue.poll());
        System.out.println("Data after Alice got polled " + trainTicketQueue);

        System.out.println("--PriorityQueue with MAX heap logic--");
        // so we want the higher priority on the reverse order of alphabets/ numbers
        // 1. Declaration
        Queue<String> fruits = new PriorityQueue<>(Comparator.reverseOrder());

        // 2. Add data
        fruits.offer("apple");
        fruits.offer("orange");
        fruits.offer("banana");
        fruits.offer("pear");
        fruits.offer("grapes");

        // At this point of time pear should get the high priority
        System.out.println(fruits);
        System.out.println("Peek() result : " + fruits.peek());

        // remove data
        System.out.println("Poll() result : " + fruits.poll());
        System.out.println("Peek() after pear got polled : " + fruits.peek());
        System.out.println(fruits);
    }
}
```


## Use cases
- Task Scheduling : can be used to schedule task based on priority
- Graph Algorithm : is often used in algorithms like Dijkstra's shortest path algorithm.
