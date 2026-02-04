# Volatile

In Java, the `volatile` keyword is used as a tool for **thread safety**. Specifically, it ensures that changes made by one thread to a shared variable are immediately visible to all other threads.

Without `volatile`, modern CPUs might cache variables in local registers or caches for performance, leading to a situation where one thread modifies a value but another thread continues to see the "stale" (old) version.

### 1. The Core Benefits

* **Visibility:** It guarantees that every read of a volatile variable will be from the main memory, and every write will be performed directly to the main memory.
* **Ordering:** It prevents the compiler and JVM from reordering code around the volatile variable, which can be crucial for initialization logic.

---

### 2. Code Example: The Shutdown Flag

Imagine a background thread that keeps running until a `stopRequested` flag is set to `true`. Without `volatile`, the background thread might never see the update from the main thread because it has cached the flag's value.

```java
public class SharedResource {
    // Without volatile, the reader thread might run forever
    private volatile boolean stopRequested = false;

    public void startWorking() {
        System.out.println("Worker thread starting...");
        while (!stopRequested) {
            // Keep doing work
        }
        System.out.println("Worker thread stopped.");
    }

    public void stop() {
        stopRequested = true;
    }

    public static void main(String[] args) throws InterruptedException {
        SharedResource resource = new SharedResource();

        // Start the worker thread
        new Thread(resource::startWorking).start();

        // Let it run for 1 second
        Thread.sleep(1000);

        // Signal to stop
        System.out.println("Main thread requesting stop...");
        resource.stop();
    }
}

```

---

### 3. Key Limitations (The "Gotcha")

It is a common mistake to think `volatile` can replace `synchronized`. It cannot.

* **Visibility  Atomicity:** `volatile` only ensures you see the latest value. It does **not** make compound operations atomic.
* **Example:** The operation `count++` is actually three steps: read, increment, and write. If two threads do this simultaneously on a `volatile int`, they might both read "5" and both write "6", losing one increment.

| Feature | `volatile` | `synchronized` |
| --- | --- | --- |
| **Visibility** | Yes | Yes |
| **Atomicity** | No | Yes |
| **Locking** | No (Non-blocking) | Yes (Blocking) |
| **Usage** | Variables only | Methods and Blocks |

---

### When to Use It?

Use `volatile` when you have a variable that is accessed by multiple threads where **at least one thread writes** to it and the others **only read** it, or when the new value does not depend on the previous value (like a simple flag).

