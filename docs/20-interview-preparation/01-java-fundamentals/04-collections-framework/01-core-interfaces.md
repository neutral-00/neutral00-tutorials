# Core Interfaces in the Collections Framework

The **Collections Framework** in Java provides a set of interfaces and classes to store and manipulate groups of objects. The core interfaces define the basic structure and behavior of collections.

---

## 1. Core Interfaces Overview
The main interfaces in the Collections Framework are:
1. **Collection**: The root interface for most collections.
2. **List**: An ordered collection (sequence) that allows duplicate elements.
3. **Set**: A collection that does not allow duplicate elements.
4. **Queue**: A collection used to hold elements prior to processing.
5. **Deque**: A double-ended queue that allows insertion and removal from both ends.
6. **Map**: A collection of key-value pairs.

---

## 2. Core Interfaces and Their Characteristics

| Interface   | Description                                      | Key Implementations                     |
|-------------|--------------------------------------------------|------------------------------------------|
| `Collection`| Root interface for most collections.            | `ArrayList`, `HashSet`, `LinkedList`     |
| `List`      | Ordered collection that allows duplicates.       | `ArrayList`, `LinkedList`, `Vector`      |
| `Set`       | Unordered collection that does not allow duplicates. | `HashSet`, `LinkedHashSet`, `TreeSet` |
| `Queue`     | Collection used for holding elements prior to processing. | `PriorityQueue`, `LinkedList`           |
| `Deque`     | Double-ended queue for insertion/removal at both ends. | `ArrayDeque`, `LinkedList`             |
| `Map`       | Collection of key-value pairs.                  | `HashMap`, `LinkedHashMap`, `TreeMap`   |

---

## 3. Hierarchy of Core Interfaces

### Diagram:
```
Collection
├── List
│     ├── ArrayList
│     ├── LinkedList
│     └── Vector
├── Set
│     ├── HashSet
│     ├── LinkedHashSet
│     └── TreeSet
├── Queue
│     ├── PriorityQueue
│     └── LinkedList
└── Deque
      ├── ArrayDeque
      └── LinkedList

Map
├── HashMap
├── LinkedHashMap
└── TreeMap
```

---

## 4. Examples of Core Interfaces

### Example of `List`:
```java
import java.util.ArrayList;
import java.util.List;

public class ListExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Apple");
        list.add("Grapes");
        list.add("Banana");
        list.add("Apple"); // Allows duplicates
        list.add("Orange");
        System.out.println(list); // Output: [Apple, Banana, Apple]

        // iterate through the list - using for-each loop
        for (String item : list) {
            System.out.println(item);
        }

        // iterate through the list - using for loop with index
        for (int i = 0; i < list.size(); i++) {
            System.out.println("Item at index " + i + ": " + list.get(i));
        }

        // accessing elements by index
        String firstItem = list.get(0);
        System.out.println("First item: " + firstItem);

        // removing an element
        list.remove("Apple"); // removes the first occurrence of "Apple"
        System.out.println("After removal: " + list);

        // removing an element by index
        list.remove(0); // removes the element at index 0
        System.out.println("After removing index 0: " + list);

        // find an element
        boolean containsBanana = list.contains("Banana");
        System.out.println("List contains Banana: " + containsBanana);

        // sorting the list
        list.sort(String::compareTo);
        System.out.println("Sorted list: " + list);
    }
}
```

### Example of `Set`:
```java
import java.util.HashSet;
import java.util.Set;

public class SetExample {
    public static void main(String[] args) {
        Set<String> set = new HashSet<>();
        set.add("Apple");
        set.add("Grapes");
        set.add("Banana");
        set.add("Apple"); // Duplicate, will not be added
        System.out.println(set); // Output: [Apple, Banana]

        // iterate through the set - using for-each loop
        for (String item : set) {
            System.out.println(item);
        }

        // iterate through the set - using forEach method with lambda
        set.forEach(item -> System.out.println(item));

        // accessing elements (no index, so we check existence)
        // Note: Sets do not support indexed access
        
        // check if an element exists
        boolean containsBanana = set.contains("Banana");
        System.out.println("Set contains Banana: " + containsBanana);

        // removing an element
        set.remove("Apple");
        System.out.println("After removal: " + set);

        // removing a non-existing element (no error)
        set.remove("Pineapple");
        System.out.println("After trying to remove non-existing element: " + set);

        // size of the set
        int size = set.size();
        System.out.println("Size of the set: " + size);

        // clear the set
        set.clear();
        System.out.println("After clearing, size of the set: " + set.size());
    }
}
```

### Example of `Map`:
```java
import java.util.HashMap;
import java.util.Map;

public class MapExample {
    public static void main(String[] args) {
        Map<Integer, String> map = new HashMap<>();
        map.put(1, "Apple");
        map.put(2, "Banana");
        map.put(1, "Orange"); // Key 1 is updated
        map.put(3, "Grapes");
        System.out.println(map); // Output: {1=Orange, 2=Banana, 3=Grapes}

        // iterate through the map - using for-each loop
        for (Map.Entry<Integer, String> entry : map.entrySet()) {
            System.out.println("Key: " + entry.getKey() + ", Value: " + entry.getValue());
        }

        // iterate through the map - using forEach method with lambda
        map.forEach((key, value) -> System.out.println("Key: " + key + ", Value: " + value));

        // accessing elements by key
        String valueForKey1 = map.get(1);
        System.out.println("Value for key 1: " + valueForKey1);

        // removing an element by key
        map.remove(2);
        System.out.println("After removal: " + map);

        // check if a key exists
        boolean containsKey3 = map.containsKey(3);
        System.out.println("Map contains key 3: " + containsKey3);

        // check if a value exists
        boolean containsValueBanana = map.containsValue("Banana");
        System.out.println("Map contains value Banana: " + containsValueBanana);

        // size of the map
        int size = map.size();
        System.out.println("Size of the map: " + size);

        // copying the map
        Map<Integer, String> copyMap = new HashMap<>(map);
        System.out.println("Copied map: " + copyMap);

        // clear the map
        map.clear();
        System.out.println("After clearing, size of the map: " + map.size());
        System.out.println("Copied map remains unchanged: " + copyMap);
    }
}
```

## Summary
| Interface   | Allows Duplicates | Maintains Order | Key-Value Pair | Example Implementation     |
|-------------|-------------------|-----------------|----------------|-----------------------------|
| `List`      | Yes               | Yes             | No             | `ArrayList`, `LinkedList`   |
| `Set`       | No                | No              | No             | `HashSet`, `TreeSet`        |
| `Queue`     | Depends           | Yes (FIFO)      | No             | `PriorityQueue`             |
| `Deque`     | Depends           | Yes             | No             | `ArrayDeque`                |
| `Map`       | No (keys only)    | No              | Yes            | `HashMap`, `TreeMap`        |

