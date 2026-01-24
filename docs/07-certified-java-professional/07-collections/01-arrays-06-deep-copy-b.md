# Deep Copy with Nested Object

When an object contains another object (like `Employee` having an `Address`), we call this **Nested Objects**.

To perform a true deep copy in this scenario, you must perform a "nested" instantiation. If you only create a new `Employee` but assign it the **old** `Address` reference, you’ve only done a partial deep copy—the address would still be shared!

---

### 1. The Model Setup (With Copy Constructors)

The cleanest way to handle this is to give both `Address` and `Employee` a **copy constructor**. This encapsulates the cloning logic inside the class itself.

```java
public class Address {
    private String city;
    private String zip;

    // Standard Constructor
    public Address(String city, String zip) {
        this.city = city;
        this.zip = zip;
    }

    // Copy Constructor for Address
    public Address(Address other) {
        this.city = other.city;
        this.zip = other.zip;
    }
    // Getters/Setters...
}

public class Employee {
    private String name;
    private Address address;

    public Employee(String name, Address address) {
        this.name = name;
        this.address = address;
    }

    // Copy Constructor for Employee
    public Employee(Employee other) {
        this.name = other.name;
        // CRITICAL: Create a NEW Address instance here!
        this.address = new Address(other.address); 
    }
    // Getters/Setters...
}

```

---

### 2. The Deep Copy using Streams

Now that our models know how to copy themselves, the Stream logic remains incredibly simple and elegant.

```java
public static void showNestedDeepCopy() {
    Address london = new Address("London", "SW1A");
    Employee alice = new Employee("Alice", london);
    
    Employee[] employees = { alice };

    // Deep Copying the array AND the nested Address
    Employee[] deepCopy = Arrays.stream(employees)
            .map(Employee::new) // Uses the Employee copy constructor
            .toArray(Employee[]::new);

    // Test: Change the city in the COPIED array
    deepCopy[0].getAddress().setCity("Manchester");

    System.out.println("Original City: " + employees[0].getAddress().getCity()); 
    // Output: London (Safe!)
    
    System.out.println("Copied City: " + deepCopy[0].getAddress().getCity());   
    // Output: Manchester
}

```

---

### Why this matters

If you had written `this.address = other.address` in the `Employee` copy constructor instead of `new Address(other.address)`, you would have a **Shallow Copy of the Address**.

In that case, changing the city to "Manchester" in the copy would have also changed Alice's original city to "Manchester," which is exactly the bug we want to avoid in multi-threaded or complex applications.

### Summary of the "Deep Chain"

* **Array Level:** `Arrays.stream()...toArray()` creates a new array container.
* **Object Level:** `new Employee(other)` creates a new Employee instance.
* **Nested Level:** `new Address(other.address)` creates a new Address instance.

---

### A Final Thought: Serialization

If your objects are 10 levels deep, writing copy constructors for everything is exhausting. In those cases, developers often use **JSON Serialization** (like Jackson or Gson):

1. Convert the object to a JSON string.
2. Convert that string back into a new Object.
*This automatically creates a 100% deep copy of everything, though it is slightly slower.*

