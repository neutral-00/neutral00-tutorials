# ArrayList

## Problem with Arrays

Arrays are fast but they have a major weakness that size cannot be changed.

## Solution - ArrayList

ArrayList is a growable array. It handles the resizing behind the scenes.
It is also part of the Java Collections Framework.

## Example
**Note:**
- Collections work with objects


## common methods

1. `add(E e)` : appends the element at the end of the list
2. `add(int, E e)` : inserts the element at the specified position
3. `remove(int i)` : removes the element at i.
4. `remove(Object o)` : removes the first occurence of o
5. `get(int i)` : gets the element at i index.
6. `set(int i, E e)` : replaces the element at i index with e.
7. `contains(Object o)` : returns true is o is present.
8. `indexOf(Object o)`: returns index of first occurence of o.
9. `size()` : returns the number of elements.
10. `isEmpty()` : returns true is list is empty.
11. `clear()` : empties the list
12. `subList(int fromIndex, int toIndex)` : returns a sublist from index fromIndex to toIndex-1. 

For code example check `practice-java` project and the class `org.lousing.collections.ArrayListExample`

```java

package org.lousing.collections;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Iterator;
import java.util.function.Predicate;

/**
 * Info : when 11th element is added size will increase by n + n/2 + 1
 * i.e. 10 + 10/2 + 1 = 16
 * internally a new array of size 16 is created and data is copied the new array
 * old array is dumped.
 * on adding 17th element it will be 16 + 8 + 1 = 25
 */

public class ArrayListExample {
    public static void showDemo() {
        // 1. Declaration and Initialization
        var flowers = new ArrayList<String>(); // creates an empty array in memory

        //2. Add data
        flowers.add("Mary Gold"); // with the first add, an array of size 10 will get created
        flowers.add("Golden Wattle");
        flowers.add("Bird of Paradise");
        flowers.add("Bougainvillea");
        // other ways to add
        var newFlowers = Arrays.asList("Jasmine", "Sunflower", "Hibiscus");
        flowers.addAll(newFlowers);
        // add at a specific index
        flowers.add(5, "Roses");
        System.out.println("Flowers after adding Rose at 5th index " + flowers);
        // 3. Getting data
        System.out.println("5th flower: " + flowers.get(5));

        // 4. Update an element
        flowers.set(5, "Rose");

        // 5. Remove data - 2nd flower
        flowers.remove(1);
        System.out.println("Removed 2nd flower");

        // 6. check Rose is still present
        System.out.println("Rose still present : " + flowers.contains("Rose"));

        // 5. Iterate
        System.out.println("---Looping the flowers with enhanced for---");
        for (String flower : flowers) {
            System.out.println(flower);
        }

        System.out.println("---Looping with forEach and lambda---");
        flowers.forEach(f -> System.out.println(f));

        System.out.println("---Iterating using Iterator---");
        Iterator<String> it = flowers.iterator();
        while (it.hasNext()){
            System.out.println(it.next());
        }
    }
}
```
