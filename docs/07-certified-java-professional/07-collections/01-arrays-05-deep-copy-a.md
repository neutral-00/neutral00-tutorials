# Array Deep Copy - Part A

Using Java Streams makes the deep copy logic much more declarative and readable. Instead of managing loop indices, you treat the array as a "flow" of data, transform each element, and collect them back into a new array.

Here is how you would implement it using your `Employee` model.

### The Streams Implementation

```java
package org.lousing.collections;

import org.lousing.model.Employee;
import java.util.Arrays;

public class ArrayStreamDeepCopy {

    public static void showDemo() {
        Employee alice = new Employee("Alice", "HR", 50_000);
        Employee bob = new Employee("Bob", "SSE", 70_000);
        Employee[] employees = {alice, bob};

        // The Stream way to Deep Copy
        Employee[] deepCopy = Arrays.stream(employees)
                .map(e -> new Employee(e.getName(), e.getDepartment(), e.getSalary()))
                .toArray(Employee[]::new);

        // Test independence
        deepCopy[0].setSalary(85_000);

        System.out.println("Original salary: " + employees[0].getSalary()); // 50,000
        System.out.println("Stream Deep Copied: " + deepCopy[0].getSalary()); // 85,000
    }
}

```

---

### Breaking Down the Pipeline

1. **`Arrays.stream(employees)`**: Converts your array into a stream of `Employee` objects.
2. **`.map(...)`**: This is the heart of the deep copy. For every employee in the stream, we "map" it to a **new** `Employee` instance. This creates the new memory allocation that prevents the shallow copy issue.
3. **`.toArray(Employee[]::new)`**: This collects the newly created objects back into a fresh array. The `Employee[]::new` is a **constructor reference** telling the stream exactly what type of array to build.

---

### When to Use Each Approach

| Method | Best Use Case |
| --- | --- |
| **Manual `for` Loop** | Performance-critical code (avoids stream overhead). |
| **Java Streams** | Readability and clean code (standard in modern Java). |
| **Serialization** | For extremely complex objects with nested lists or trees where manual mapping is too difficult. |

---

### Pro-Tip: Deep Copying a List

If you were using an `ArrayList` instead of a basic array, the syntax is even more common in professional projects:

```java
List<Employee> deepCopyList = originalList.stream()
    .map(Employee::new) // Assumes you have a Copy Constructor!
    .toList();

```

