# Implementations in the Collections Framework

The **Collections Framework** in Java provides various concrete implementations of the core interfaces. These implementations are optimized for different use cases, such as performance, ordering, and thread-safety.

---

## 1. List Implementations
The `List` interface has the following common implementations:

| Implementation   | Description                                      | Key Features                          |
|------------------|--------------------------------------------------|---------------------------------------|
| `ArrayList`      | Resizable array implementation.                  | Fast random access, not thread-safe.  |
| `LinkedList`     | Doubly-linked list implementation.               | Fast insertion/deletion, not thread-safe. |
| `Vector`         | Synchronized resizable array.                    | Thread-safe, slower than `ArrayList`. |

### Example:
```java
import java.util.ArrayList;
import java.util.List;

public class ArrayListExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Apple");
        list.add("Banana");
        System.out.println(list); // Output: [Apple, Banana]
    }
}
```

## 2. Set Implementations
The `Set` interface has the following common implementations:

| Implementation   | Description                                      | Key Features                          |
|------------------|--------------------------------------------------|---------------------------------------|
| `HashSet`        | Hash table based implementation.                 | Fast access, no duplicates, not thread-safe. |

### Example:
```java
import java.util.HashSet;
import java.util.Set;

public class HashSetExample {
    public static void main(String[] args) {
        Set<String> set = new HashSet<>();
        set.add("Apple");
        set.add("Banana");
        set.add("Apple"); // Duplicate, will not be added
        System.out.println(set); // Output: [Apple, Banana]
    }
}
```

## 3. Map Implementations
The `Map` interface has the following common implementations:

| Implementation   | Description                                      | Key Features                          |
|------------------|--------------------------------------------------|---------------------------------------|
| `HashMap`        | Hash table based implementation.                 | Fast access, allows null keys/values, not thread-safe. |

### Example:
```java
import java.util.HashMap;
import java.util.Map;

public class HashMapExample {
    public static void main(String[] args) {
        Map<Integer, String> map = new HashMap<>();
        map.put(1, "Apple");
        map.put(2, "Banana");
        map.put(1, "Orange"); // Key 1 is updated
        System.out.println(map); // Output: {1=Orange, 2=Banana}
    }
}
```

## 4. Queue Implementations
The `Queue` interface has the following common implementations:

| Implementation       | Description                                      | Key Features                          |
|----------------------|--------------------------------------------------|---------------------------------------|
| `PriorityQueue`      | Priority queue based on a priority heap.         | Elements are ordered by their natural ordering or by a comparator. |

### Example:
```java
import java.util.PriorityQueue;
import java.util.Queue;

public class PriorityQueueExample {
    public static void main(String[] args) {
        Queue<Integer> queue = new PriorityQueue<>();
        queue.add(10);
        queue.add(5);
        queue.add(20);
        System.out.println(queue); // Output: [5, 10, 20]
    }
}
```

## 5. Deque Implementations
The `Deque` interface has the following common implementations:

| Implementation       | Description                                      | Key Features                          |
|----------------------|--------------------------------------------------|---------------------------------------|
| `ArrayDeque`         | Resizable-array implementation of the `Deque` interface. | Fast insertion/removal at both ends, not thread-safe. |

### Example:
```java
import java.util.ArrayDeque;
import java.util.Deque;

public class ArrayDequeExample {
    public static void main(String[] args) {
        // Create an ArrayDeque
        Deque<String> deque = new ArrayDeque<>();

        // Add elements to the deque
        deque.addFirst("First");
        deque.addLast("Last");
        deque.add("Middle"); // Adds to the end by default

        // Display the deque
        System.out.println("Deque: " + deque); // Output: [First, Last, Middle]

        // Access elements
        System.out.println("First Element: " + deque.getFirst()); // Output: First
        System.out.println("Last Element: " + deque.getLast());   // Output: Middle

        // Remove elements
        deque.removeFirst();
        deque.removeLast();

        // Display the deque after removals
        System.out.println("Deque after removals: " + deque); // Output: [Last]
    }
}
```

## Summary
| Interface   | Implementation   | Key Features                          |
|-------------|------------------|---------------------------------------|
| `List`      | `ArrayList`      | Fast random access, not thread-safe.  |
|             | `LinkedList`     | Fast insertion/deletion, not thread-safe. |
|             | `Vector`         | Thread-safe, slower than `ArrayList`. |
| `Set`       | `HashSet`        | Fast access, no duplicates, not thread-safe. |
|             | `LinkedHashSet`  | Maintains insertion order, no duplicates. |
|             | `TreeSet`        | Sorted order, no duplicates.          |
| `Map`       | `HashMap`        | Fast access, allows null keys/values, not thread-safe. |
|             | `LinkedHashMap`  | Maintains insertion order, allows null keys/values. |
|             | `TreeMap`        | Sorted by keys, does not allow null keys. |
| `Queue`     | `PriorityQueue`  | Elements ordered by natural ordering or comparator. |
| `Deque`     | `ArrayDeque`     | Fast insertion/removal at both ends, not thread-safe. |