# Deep Copy - JSON

Using a JSON library for deep copying is often called the **"Lazy Developer's Deep Copy."** It is incredibly powerful because it doesn't care how many nested objects, lists, or maps you have—it simply serializes the entire object tree into a string and "re-inflates" it into a brand-new set of memory addresses.

In the industry, **Jackson** is the most common library used for this (it's the default in Spring Boot).

---

### 1. The Setup

To use this, you don't need copy constructors at all. You just need a library like Jackson and your classes must have a **default (no-args) constructor** and **getters/setters** so the library can read and write the data.

### 2. The Implementation

Here is how you can deep copy your `Employee` array using the Jackson `ObjectMapper`:

```java
import com.fasterxml.jackson.databind.ObjectMapper;
import org.lousing.model.Employee;

public class JsonDeepCopy {
    private static final ObjectMapper mapper = new ObjectMapper();

    public static void showDemo() {
        try {
            Employee alice = new Employee("Alice", new Address("London", "SW1A"));
            Employee[] employees = { alice };

            // 1. Serialize: Convert the whole array to a JSON String
            String jsonString = mapper.writeValueAsString(employees);

            // 2. Deserialize: Convert that String back into a NEW array
            Employee[] deepCopy = mapper.readValue(jsonString, Employee[].class);

            // Test: Deep independence
            deepCopy[0].getAddress().setCity("Manchester");

            System.out.println("Original: " + employees[0].getAddress().getCity()); // London
            System.out.println("Deep Copy: " + deepCopy[0].getAddress().getCity()); // Manchester

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}

```

---

### Pros and Cons of the JSON Approach

| Feature | Copy Constructors / Streams | JSON Serialization |
| --- | --- | --- |
| **Effort** | High (Must write logic for every class) | Low (Write once, works for all) |
| **Performance** | **Very Fast** (Direct memory allocation) | Slower (String parsing overhead) |
| **Maintenance** | Hard (Adding a field means updating constructors) | Easy (Handles new fields automatically) |
| **Best For** | Simple objects, performance-critical apps | Deeply nested, complex objects |

---

### 3. A Reusable Utility Method

If you find yourself doing this often, you can create a generic "Cloner" utility:

```java
public class DeepCopyUtils {
    private static final ObjectMapper mapper = new ObjectMapper();

    public static <T> T deepCopy(T object, Class<T> type) {
        try {
            return mapper.readValue(mapper.writeValueAsString(object), type);
        } catch (Exception e) {
            throw new RuntimeException("Deep copy failed", e);
        }
    }
}

// Usage:
Employee[] copy = DeepCopyUtils.deepCopy(employees, Employee[].class);

```

### Summary of what we've covered

We started with the `synchronized` keyword, moved through **Angular** event listeners, explored **Java Threads/Lambdas**, and finished with three ways to **Deep Copy** in Java (Manual, Streams, and JSON).

Would you like to shift gears back to **Angular** and see how to use **`@HostBinding`** (the sibling of `@HostListener`) to change styles on your host element?
