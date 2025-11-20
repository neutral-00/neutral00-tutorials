# Thread Creation in Java

There are two main ways to create and work with threads in Java:
1. Extending the `Thread` class
2. Implementing the `Runnable` interface

## 1. Extending Thread Class

This approach involves creating a subclass of the `Thread` class and overriding its `run()` method:

```java
public class MyThread extends Thread {
    @Override
    public void run() {
        // Code to be executed in the thread
        System.out.println("Thread is running: " + Thread.currentThread().getName());
    }
}

// Usage
MyThread thread = new MyThread();
thread.start(); // Don't call run() directly!
```

### Pros and Cons of Extending Thread
👍 **Pros:**
- Direct access to Thread methods
- No need for external Thread instance
- Simpler for basic threading needs

👎 **Cons:**
- Java doesn't support multiple inheritance
- Less flexible than Runnable
- Tighter coupling between task and thread

## 2. Implementing Runnable Interface

This is the preferred approach as it provides better separation of concerns:

```java
public class MyRunnable implements Runnable {
    @Override
    public void run() {
        // Code to be executed in the thread
        System.out.println("Thread is running: " + Thread.currentThread().getName());
    }
}

// Usage
MyRunnable runnable = new MyRunnable();
Thread thread = new Thread(runnable);
thread.start();
```

### Modern Approach Using Lambda
Since `Runnable` is a functional interface, you can use lambda expressions (Java 8+):

```java
Thread thread = new Thread(() -> {
    System.out.println("Thread running with lambda: " + Thread.currentThread().getName());
});
thread.start();
```

### Pros and Cons of Implementing Runnable
👍 **Pros:**
- Better separation between task and thread
- Can implement multiple interfaces
- More flexible and reusable
- Works well with executor framework
- Supports functional programming (lambda)

👎 **Cons:**
- Need separate Thread instance
- No direct access to Thread methods
- Slightly more verbose for basic uses

## Important Thread Methods

```java
// Setting thread name
thread.setName("CustomThreadName");

// Setting thread priority (1-10)
thread.setPriority(Thread.MAX_PRIORITY); // 10
thread.setPriority(Thread.NORM_PRIORITY); // 5
thread.setPriority(Thread.MIN_PRIORITY); // 1

// Make thread daemon (background thread)
thread.setDaemon(true); // Must be called before start()

// Check if thread is alive
boolean isAlive = thread.isAlive();

// Get current thread
Thread currentThread = Thread.currentThread();
```

## Best Practices

1. **Prefer Runnable over Thread**
   - More flexible and reusable
   - Better supports modern concurrent programming

2. **Never Call run() Directly**
   - Always use `start()` to execute thread
   - Calling `run()` directly executes in current thread

3. **Handle InterruptedException**
   - Always handle or propagate interrupt signals
   - Helps with proper thread shutdown

4. **Use Meaningful Thread Names**
   - Helps with debugging and monitoring
   - Set names using constructor or `setName()`

5. **Consider Using Executor Framework**
   - Modern alternative to direct thread creation
   - Better for managing thread lifecycle

## Common Pitfalls

1. **Thread Safety Issues**
   ```java
   // Bad - not thread safe
   public class Counter {
       private int count = 0;
       public void increment() { count++; }
   }

   // Good - thread safe
   public class Counter {
       private AtomicInteger count = new AtomicInteger(0);
       public void increment() { count.incrementAndGet(); }
   }
   ```

2. **Resource Leaks**
   ```java
   // Bad - thread keeps running
   while(true) {
       new Thread(() -> process()).start();
   }

   // Good - use thread pool
   ExecutorService executor = Executors.newFixedThreadPool(10);
   executor.submit(() -> process());
   ```

3. **Deadlock Risk**
   ```java
   // Potential deadlock
   synchronized(lockA) {
       synchronized(lockB) {
           // ...
       }
   }

   // Better - consistent lock ordering
   synchronized(getLockInOrder(lockA, lockB)) {
       // ...
   }
   ```