# Iterators in the Collections Framework

In Java, **Iterators** are used to traverse elements in a collection. They provide a uniform way to access elements without exposing the underlying structure of the collection.

---

## 1. Types of Iterators
Java provides the following types of iterators:
1. **Iterator**: A universal iterator for all `Collection` types.
2. **ListIterator**: A bidirectional iterator for `List` types.
3. **Enumeration**: A legacy iterator for older classes like `Vector` and `Hashtable`.

---

## 2. Using `Iterator`
The `Iterator` interface provides methods to traverse a collection in a forward direction.

### Key Methods:
- `hasNext()`: Returns `true` if there are more elements to iterate.
- `next()`: Returns the next element in the iteration.
- `remove()`: Removes the last element returned by the iterator.

### Example:
```java
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

public class IteratorExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Apple");
        list.add("Banana");
        list.add("Cherry");

        Iterator<String> iterator = list.iterator();
        while (iterator.hasNext()) {
            String element = iterator.next();
            System.out.println(element);
        }
    }
}
```

---

## 3. Using `ListIterator`
The `ListIterator` interface extends `Iterator` to allow bidirectional traversal of a list.

### Key Methods:
- `hasNext()`: Returns `true` if there are more elements when traversing forward.
- `next()`: Returns the next element in the forward traversal.
- `hasPrevious()`: Returns `true` if there are more elements when traversing backward.
- `previous()`: Returns the next element in the backward traversal.
- `set(E e)`: Replaces the last element returned by this iterator with the specified element.

### Example:
```java
import java.util.LinkedList;
import java.util.List;
import java.util.ListIterator;

public class ListIteratorExample {
    public static void main(String[] args) {
        List<String> list = new LinkedList<>();
        list.add("Apple");
        list.add("Banana");
        list.add("Cherry");

        ListIterator<String> listIterator = list.listIterator();

        // Forward traversal
        while (listIterator.hasNext()) {
            System.out.println("Forward: " + listIterator.next());
        }

        // Backward traversal
        while (listIterator.hasPrevious()) {
            System.out.println("Backward: " + listIterator.previous());
        }
    }
}
```

---

## 4. Using `Enumeration`
The `Enumeration` interface is a legacy interface that is similar to `Iterator`, but it does not have a `remove` method.

### Key Methods:
- `hasMoreElements()`: Returns `true` if there are more elements to enumerate.
- `nextElement()`: Returns the next element in the enumeration.

### Example:
```java
import java.util.Enumeration;
import java.util.Vector;

public class EnumerationExample {
    public static void main(String[] args) {
        Vector<String> vector = new Vector<>();
        vector.add("Apple");
        vector.add("Banana");
        vector.add("Cherry");

        Enumeration<String> enumeration = vector.elements();
        while (enumeration.hasMoreElements()) {
            System.out.println(enumeration.nextElement());
        }
    }
}
```

## Summary
| Iterator Type   | Direction       | Key Methods                          | Applicable Collections                  |
|------------------|-----------------|--------------------------------------|-----------------------------------------|
| `Iterator`       | Forward         | `hasNext()`, `next()`, `remove()`    | All `Collection` types                  |
| `ListIterator`   | Forward/Backward| `hasNext()`, `next()`, `hasPrevious()`, `previous()`, `set(E e)` | `List` types only                       |
| `Enumeration`    | Forward         | `hasMoreElements()`, `nextElement()` | Legacy classes like `Vector`, `Hashtable` |