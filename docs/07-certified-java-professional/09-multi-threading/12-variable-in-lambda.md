# Variable in Lambda Expression

This is one of the most common "gotchas" in Java. You’ll notice that if you try to change a local variable inside a lambda that was defined outside of it, the compiler throws an error: *"Variable used in lambda expression should be final or effectively final."*

The reason for this isn't just a design choice; it’s due to how Java handles memory and threads.

---

### 1. The Technical Reason: "Variable Capture"

When you create a lambda, it doesn't actually use the "real" variable from your method. Instead, it makes a **copy** of that variable to use inside the lambda. This is called **capturing**.

* **Local variables** live on the **Stack**.
* **Lambdas (Objects)** live on the **Heap**.

The stack frame of a method disappears as soon as the method finishes. However, the lambda might be passed to a thread and run much later. If the lambda tried to access the original variable on a stack that no longer exists, the program would crash. By making a copy, the lambda stays "alive" even after the method ends.

---

### 2. The Consistency Reason

If Java allowed you to change the variable inside the lambda, you would have two different values: the one in the original method and the copy inside the lambda.

* If the original changed, the lambda wouldn't know.
* If the lambda changed its copy, the original wouldn't know.

To prevent this confusion and the bugs that come with it, Java enforces a rule: **The variable must not change.**

---

### 3. The Thread Safety Reason

Lambdas are heavily used in multi-threading (like `parallelStream` or `CompletableFuture`).

If multiple threads could modify the same local variable through a lambda, we would run into the **Race Conditions** we discussed earlier. By forcing variables to be `final`, Java ensures that lambdas are "stateless" regarding local variables, making them inherently safer for concurrency.

---

### What is "Effectively Final"?

Before Java 8, you had to explicitly write the word `final`. Since Java 8, the compiler is smarter. If you assign a value to a variable once and **never change it again**, the compiler treats it as "effectively final" even without the keyword.

```java
public void demo() {
    int port = 8080; // I didn't say final, but I never changed it.

    Runnable r = () -> System.out.println("Connecting to: " + port); 
    // Works! 'port' is effectively final.

    // port = 9090; // If I uncomment this, the lambda above will BREAK.
}

```

---

### The Workaround (If you really need to change it)

If you absolutely must change a value inside a lambda, you can wrap it in an object or an array (which live on the heap). The **reference** to the array remains final, but the **content** inside it can change.

```java
public void workaround() {
    int[] counter = {0}; // An array is an object on the heap

    Runnable r = () -> {
        counter[0]++; // This works! We aren't changing the 'counter' reference.
    };
}

```

*Note: This is generally discouraged because it is not thread-safe. Use an `AtomicInteger` instead if you are working with multiple threads!*

---

### Summary Table

| Feature | Why it must be Final |
| --- | --- |
| **Lifetime** | Local variables die when the method ends; Lambdas live longer. |
| **Storage** | Stack (variable) vs Heap (lambda). |
| **Integrity** | Ensures the copy inside the lambda matches the original. |
| **Concurrency** | Prevents race conditions on local variables. |

Would you like to see how this rule differs when using **Instance Variables** (fields in a class) instead of local variables?
