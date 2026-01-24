# Callable and Future

In Java, the biggest limitation of `Runnable` is that the `run()` method is `void`—it performs an action but cannot return a result or throw checked exceptions.

To solve this, Java introduced the **`Callable`** interface and the **`Future`** object.

---

### 1. Callable vs. Runnable

Think of `Runnable` as a "fire and forget" task, while `Callable` is a "task with a receipt."
receipt is pronounced as ruh.seet 

* **`Runnable`**: `public void run()` — Does work, returns nothing.
* **`Callable<V>`**: `public V call()` — Does work and returns a result of type `V`.

---

### 2. How to use them (with Lambdas)

Since you can't pass a `Callable` directly into a `Thread` constructor, we typically use an **`ExecutorService`**. This service manages a pool of threads for us.

```java
import java.util.concurrent.*;

public class Main {
    public static void main(String[] args) throws Exception {
        // 1. Create a thread pool
        ExecutorService executor = Executors.newSingleThreadExecutor();

        // 2. Define a task using a Lambda (Callable returns a String)
        Callable<String> task = () -> {
            Thread.sleep(2000); // Simulate work
            return "Task Complete!";
        };

        // 3. Submit the task and get a "Future" (the receipt)
        System.out.println("Submitting task...");
        Future<String> future = executor.submit(task);

        // 4. Do other work while the thread runs...
        System.out.println("Doing other things...");

        // 5. Get the result (this blocks until the thread is finished)
        String result = future.get(); 
        System.out.println("Result from thread: " + result);

        executor.shutdown();
    }
}

```

**NOTE**
- `executor.submit()` can take runnable as well as callable.

---


### 3. Understanding the `Future`

The `Future` object is a placeholder for a value that doesn't exist yet. It provides several helpful methods:

* **`get()`**: Waits (blocks) until the thread finishes and returns the result.
* **`isDone()`**: Returns `true` if the task is finished.
* **`cancel()`**: Attempts to stop the task if it's still running.

---

### Comparison Table

| Feature | `Runnable` | `Callable` |
| --- | --- | --- |
| **Method** | `run()` | `call()` |
| **Return Value** | `void` (None) | Generic Type `V` |
| **Exceptions** | Unchecked only | Can throw Checked Exceptions |
| **Execution** | `new Thread(r).start()` | `executor.submit(c)` |

---

### Modern Alternative: `CompletableFuture`

In modern Java (8+), we often use `CompletableFuture` instead of basic `Future` because it allows you to **chain** tasks together (e.g., "Once Task A finishes, pass the result to Task B") without blocking the main thread.

```java
CompletableFuture.supplyAsync(() -> "Data")
    .thenApply(data -> data + " processed")
    .thenAccept(System.out::println);

```

