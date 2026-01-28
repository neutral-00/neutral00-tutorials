# Arrays

An array is a fixed-sized data structure that holds a collection of elements of the same type.

## Declaration | Initialization | access
```java
int[] numbers = new int[5];
String[] names = {"Alice", "Bob", "Charlie"};
String n = names[1];  // Bob
int l = names.length; // size
```

## Basic Operations
- Indexing: Access or modify an element by its index, e.g. `number[0]`, `number[2] = 10`.
- Traversal: Loop over elements with a `for` loop or for-each loop.

Regular Java arrays (like `int[] numbers`) are objects of type `Array`, but they do not have built-in array-specific methods. Instead, these arrays inherit standard methods from the `Object` class:

- `clone()`: Creates a copy of the array.
- `equals(Object obj)`: Compares the array reference with another reference for equality.
- `hashCode()`: Returns a hash code for the array object.
- `toString()`: Returns a string that identifies the array type and memory address.
- `getClass()`: Returns the runtime class of the array object.

Arrays also expose one key property:
- `length`: The number of elements in the array.

Most practical manipulation (like sorting, filling, searching, copying, comparing) is done using static methods from the `java.util.Arrays` class, not directly on the array object itself.

## Useful Methods (via `Arrays` utility class)
- `Arrays.sort(number)`: Sorts the array in ascending order.
- `Arrays.copyOf(number, newLength)`: Copies the array to a new array of specified length.
- `Arrays.fill(number, value)`: Fills all elements with the given value.
- `Arrays.equals(arr1, arr2)`: Compares two arrays for equality.
- `Arrays.toString(number)`: Returns a string representation of the array.
- `Arrays.binarySearch(number, key)`: Searches for a value and returns its index (array must be sorted).
- `Arrays.copyOfRange(number, from, to)`: Copies a subrange of the array to a new array.

Regular arrays don’t have advanced methods—these are provided by the `java.util.Arrays` class and require static calls.

Example
```java

package org.lousing.andrii.collections;

import java.util.Arrays;

public class ArraysExample {

  public static void showDemo() {
    int[] numbers = new int[2];
    double[] doubles = new double[2];
    boolean[] booleans = new boolean[2];

    System.out.println("numbers[1] : " + numbers[0]); // 0
    System.out.println("doubles[0] : " + doubles[0]); // 0.0
    System.out.println("booleans[0] : " + booleans[0]); // false
    System.out.println("numbers.length : " + numbers.length);

    // array literals
    int[] someInts = { 16, 8, 32 };
    // multi dimensional array
    int[][] matrix = {
        { 1, 4, 8 },
        { 3, 9, 12 }
    };
    System.out.println("matrix[1][1] : " + matrix[1][1]);

    // print and sort arrays - using java.util.Arrays class
    System.out.println(Arrays.toString(someInts));
    Arrays.sort(someInts);
    System.out.println("After sorting");
    System.out.println(Arrays.toString(someInts));

  }
}
```
```
```
