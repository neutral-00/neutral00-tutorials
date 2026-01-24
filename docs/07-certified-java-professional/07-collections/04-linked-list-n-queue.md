# LinkedList

In a `LinkedList`, elements are not stored in a continuous block of memory. \
Instead it is wrapped in a Node.

A Node has 3 parts:
1. Data: The actual value.
2. Next: A reference to the next Node in the chain.
3. Previous: A reference to the previous node in case of Doubley LinkedList

**NOTE**
- Both the LinkedList and ArrayList implements the List Interface
- So both shares a list common methods

```java

package org.lousing.collections;

import java.sql.SQLOutput;
import java.util.LinkedList;
import java.util.List;
import java.util.Queue;

public class LinkedListExample {

    public static void  showDemo() {
        System.out.println("--LinkedList Queue Example--");
        // 1. Declare and initialize
        Queue<String> ticketQueue = new LinkedList<>();

        // 2. Add data |
        // offer method returns true on success and false on failure
        // add method will return true on success and throw error on failure
        System.out.println(ticketQueue.offer("Alice"));
        System.out.println(ticketQueue.add("Charlie"));
        System.out.println(ticketQueue.add("Bob"));

        System.out.println(ticketQueue);

        // 3. remove data using the poll method
        System.out.println("Poll() result : " + ticketQueue.poll());
        System.out.println("Peek() after polled Alice : " + ticketQueue.peek());
        // you can remove data using remove but will throw error when empty
        System.out.println("Remove() result : " + ticketQueue.remove());
        // you can see the next element to be removed from the queue using peek or element
        // difference is peek will return null when empty
        // while element will throw error when queue is empty
        System.out.println("element() result : " + ticketQueue.element());
        // If you want to avoid runtime errors
        // use offer,poll,peek methods in place of add, remove, element methods respectively

        System.out.println("--LinkedList As List Example--");
        // 1. Declaration and Initialization
        List<String> students = new LinkedList<>();

        // 2. add data - all the operations learnt in ArrayList apply here
        students.add("Shiva");
        students.add("Ram");
        students.add("Sita");
        System.out.println(students);

        // 3. LinkedList specific methods
        // adding to the start or end is superfast
        students.addFirst("Robin");
        students.addLast("Damien");
        System.out.println("Data after adding Robin and Damien in the first and last : ");
        System.out.println(students);
        // similarly you can use removeFirst and removeLast methods

        // 4. Accessing
        System.out.println("2nd Student : " + students.get(1));

        // 5. Printing using lambda
        students.forEach(System.out::println);

    }
}
```

## When To Prefer LinkedList over ArrayList

It all comes down to time complexity.
- get by index - winner is ArrayList | LinkedList has to walk the chain
- add/remove at the end - can say tie
- add/remove at the start - LinkedList is the winner | ArrayList must shift all the items
- memory uage - ArrayList is the winner | LinkedList needs space for data + pointers

### Prefer ArrayList when you need
1. frequest access by index
2. memory to be compact
3. to add data mostly at the end

### Prefer LinkedList when
1. you add or remove items from the start or middle
2. you care only the ends of like like queue or stack

**NOTE**
- Modern CPUs are incredibly good at moving continuous blocks of memory. 
- Most professional default to ArrayList
