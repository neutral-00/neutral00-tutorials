# Thread - Lambda

Before Lambdas, threads were created using anonymous classes.

---

### 1. Before Lambdas: The Anonymous Class Era

Before Java 8, if you wanted to run code in a new thread, you had to implement the `Runnable` interface using an **Anonymous Inner Class**. It required a lot of boilerplate code just to define one simple action.

```java
// The "Old Way"
Thread thread = new Thread(new Runnable() {
    @Override
    public void run() {
        System.out.println("Thread is running the old-fashioned way!");
    }
});

thread.start();

```

**The Problem:** You had to explicitly write `new Runnable()`, `@Override`, and `public void run()` every single time. The actual logic (the `println`) was buried inside 5 lines of "syntax noise."

---

### 2. After Lambdas: The Modern Way

Since `Runnable` is a **Functional Interface** (it only has one abstract method: `run()`), Java 8 allowed us to replace that entire block with a Lambda expression `() -> { ... }`.

```java
// The "Modern Way" (Lambda)
Thread thread = new Thread(() -> {
    System.out.println("Thread is running with a Lambda!");
});

thread.start();

```

If the code is only one line, you can make it even shorter:

```java
Thread thread = new Thread(() -> System.out.println("Short and sweet!"));
thread.start();

```

---

### How the "Magic" Works

When you use a Lambda, the Java compiler looks at the `Thread` constructor. It sees that it expects a `Runnable` object. Because a Lambda matches the signature of the `run()` method (no parameters, returns void), the compiler automatically "wraps" your Lambda into a `Runnable` for you.

---

### Key Differences at a Glance

| Feature | Anonymous Inner Class (Old) | Lambda Expression (Modern) |
| --- | --- | --- |
| **Verbosity** | Very high (Boilerplate) | Very low (Concise) |
| **File Size** | Creates a separate `.class` file | Handled via `invokedynamic` (more efficient) |
| **Scope** | `this` refers to the Anonymous class | `this` refers to the enclosing class |
| **Readability** | Logic is often buried | Logic is front and center |

---

**NOTE**
- Variable used in lambda expression should be final or effectively final
- What does it mean?
- see the next tutorial



### A Step Further: Method References

If your thread is just calling an existing method, you can use the **double colon (`::`)** operator for the ultimate shorthand:

```java
// Assuming you have a method named printMessage
Thread thread = new Thread(this::printMessage);
thread.start();

```

Would you like to see how to handle **returning a value** from a thread using `Callable` and `Future`, since `Runnable` can't return results?
