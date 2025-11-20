# Comparators in the Collections Framework

In Java, **comparators** are used to define custom sorting logic for objects. They are part of the `java.util` package and are commonly used with collections like `TreeSet`, `TreeMap`, and sorting methods like `Collections.sort()`.

---

## 1. Comparator vs Comparable
Java provides two interfaces for sorting:
1. **`Comparable`**: Used to define the natural ordering of objects.
2. **`Comparator`**: Used to define custom ordering of objects.

| Feature          | `Comparable`                          | `Comparator`                          |
|-------------------|---------------------------------------|---------------------------------------|
| Package           | `java.lang`                          | `java.util`                           |
| Method            | `compareTo(Object o)`                | `compare(Object o1, Object o2)`       |
| Sorting Logic     | Defined in the class itself.          | Defined in a separate class.          |
| Use Case          | Natural ordering.                    | Custom ordering.                      |

---

## 2. Using `Comparator` for Custom Sorting

### Example:
```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;
import java.util.List;

class Student {
    String name;
    int age;

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return name + " (" + age + ")";
    }
}

class AgeComparator implements Comparator<Student> {
    @Override
    public int compare(Student s1, Student s2) {
        return Integer.compare(s1.age, s2.age);
    }
}

public class ComparatorExample {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("Alice", 22));
        students.add(new Student("Bob", 20));
        students.add(new Student("Charlie", 21));

        // Sort by age using Comparator
        Collections.sort(students, new AgeComparator());
        System.out.println(students); // Output: [Bob (20), Charlie (21), Alice (22)]
    }
}
```

### 3 Using Lambda Expressions with Comparator
Java 8 introduced lambda expressions, which provide a concise way to represent functional interfaces (like `Comparator`).

#### Example:
```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class LambdaComparatorExample {
    public static void main(String[] args) {
        List<String> names = new ArrayList<>();
        names.add("Alice");
        names.add("Bob");
        names.add("Charlie");

        // Sort in reverse order using a lambda expression
        Collections.sort(names, (a, b) -> b.compareTo(a));
        System.out.println(names); // Output: [Charlie, Bob, Alice]
    }
}
```

## Comparable Example
```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

class Student implements Comparable<Student> {
    String name;
    int age;

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public int compareTo(Student other) {
        return Integer.compare(this.age, other.age); // Natural ordering by age
    }

    @Override
    public String toString() {
        return name + " (" + age + ")";
    }
}

public class ComparableExample {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student("Alice", 22));
        students.add(new Student("Bob", 20));
        students.add(new Student("Charlie", 21));

        // Sort using Comparable
        Collections.sort(students);
        System.out.println(students); // Output: [Bob (20), Charlie (21), Alice (22)]
    }
}
```
### Key Points:
The Student class implements the Comparable interface.
The compareTo method defines the natural ordering (by age in this case).
The Collections.sort() method uses the natural ordering defined in the compareTo method.