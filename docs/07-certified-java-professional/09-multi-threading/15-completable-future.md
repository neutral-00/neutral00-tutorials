# Completable Future

**`CompletableFuture`** is used for asynchronous programming in Java.
Asynchronous programming is writing non-blocking code that runs on a separate thread rather than the main thread.

It was introduced in Java 8 to handle the limitations of Future class.

Future is a reference to the result of an asynchronous computation.

## Limitations of Future
1. It can not be completed manually.
1. It provides a get method which blocks until the result is available.
1. It doesn't have the feature to attach a callback.
1. Multiple futures can not be chained together.
1. We can't have multiple futures run in parallel and then run some code after all of them completes.
1. There is no exception handling in the Future API.


Chaining is useful when we need to execute a long running task and when the task is done, we need to send the result to another long running task and so on.

`CompletableFuture` implements `Future` and `CompletionStage` interface.




If the original `Future` was a "receipt" for a task, `CompletableFuture` is like a **smart workflow engine**.

It allows you to chain tasks, handle errors gracefully, and combine results from multiple threads without ever calling `.get()` and blocking your main application.

---

### Why we use it "Nowadays" (The "Promise" of Java)

If you've used JavaScript, `CompletableFuture` is essentially Java's version of a **Promise**. In modern high-scale applications (like those using Spring Boot), we use it to achieve **concurrency** without the overhead of waiting for threads to finish.

#### Key Modern Features:

* **Non-Blocking Pipelines:** You can define a whole sequence of events (e.g., "Fetch Data"  "Transform It"  "Save to DB") that runs entirely in the background.
* **Exception Management:** It has built-in methods like `.exceptionally()` to catch errors in the background and provide "fallback" values so the whole app doesn't crash.
* **Parallel Coordination:** You can easily wait for *all* tasks to finish (`allOf`) or take the result of the *first* one to finish (`anyOf`).

---

### Real-World Use Cases

#### 1. Microservices Data Aggregation (API Gateway)

Imagine a "Product Detail" page on Amazon. To load that page, the backend must fetch:

1. **Product Info** (Service A)
2. **Price & Discounts** (Service B)
3. **User Reviews** (Service C)
4. **Stock Availability** (Service D)

Instead of calling these one-by-one (taking 4 seconds), you trigger all 4 simultaneously using `CompletableFuture.supplyAsync()`. You then use `CompletableFuture.allOf()` to combine them. The total time taken is only as long as the **slowest single service**.

#### 2. Order Processing Pipeline

In e-commerce, once a user clicks "Buy," several **dependent** steps must happen in order:

* `validateOrder()`  `processPayment()`  `sendEmailConfirmation()`
Using `.thenCompose()`, you can chain these so that `processPayment` only starts after `validateOrder` succeeds, all without blocking the web server thread.

#### 3. High-Frequency Logging or Analytics

In a payment gateway, you don't want to make a customer wait while you write a log to a slow database. You can use `CompletableFuture.runAsync()` to "fire and forget" the logging task in a background thread pool, allowing the customer's transaction to finish instantly.

---

### Quick Code Comparison: Future vs. CompletableFuture

| Feature | `Future` (Java 5) | `CompletableFuture` (Java 8+) |
| --- | --- | --- |
| **Manual Completion** | No | Yes (`.complete(value)`) |
| **Chaining Tasks** | No (Must block and wait) | Yes (`.thenApply()`, `.thenAccept()`) |
| **Error Handling** | Basic try-catch | Fluent (`.exceptionally()`) |
| **Combining** | Manual/Difficult | Easy (`.thenCombine()`, `.allOf()`) |

---

### Modern Chaining Example

```java
CompletableFuture.supplyAsync(() -> fetchUser(id))
    .thenApply(user -> user.getName().toUpperCase()) // Transform result
    .thenAccept(name -> System.out.println("Hello, " + name)) // Consume result
    .exceptionally(ex -> {
        System.err.println("Error: " + ex.getMessage());
        return null; // Fallback
    });

```

Would you like to see how to use **`CompletableFuture.allOf()`** to wait for multiple independent API calls to finish at the same time?

[Introduction to CompletableFuture in Java 8](https://www.youtube.com/watch?v=ImtZgX1nmr8)
This video provides a solid foundation for understanding how CompletableFuture enables asynchronous reactive programming models in Java.
