# ReentrantLock


```java
package org.lousing.multithreading;

import java.util.concurrent.locks.ReentrantLock;

public class ReentrantExample {
    final ReentrantLock lock = new ReentrantLock();

    public void firstMethod() {
        lock.lock();
        try {
            System.out.println("Inside firstMethod");
            secondMethod();
        }finally {
            lock.unlock();
        }
    }

    public void secondMethod() {
        lock.lock();
        try {
            System.out.println("Inside secondMethod");
        } finally {
            lock.unlock();
        }
    }

    public static void showDemo() {
        ReentrantExample re = new ReentrantExample();
        re.firstMethod();
    }
}
```

This code demonstrates a fundamental concept in Java concurrency called **Reentrancy**. It shows how a thread can acquire the same lock multiple times without blocking itself (deadlocking).

Here is a breakdown of what is happening step-by-step:

### 1. The Core Concept: Reentrancy

In many locking systems, if a thread holds a lock and tries to acquire it again, it would get stuck waiting for itself to release the lock. However, Java’s `ReentrantLock` allows a thread to "re-enter" a lock it already holds.

### 2. Execution Flow

When `showDemo()` is called, the following sequence occurs:

1. **`firstMethod()` starts:** The thread calls `lock.lock()`. Since no one else holds the lock, it acquires it. The **hold count** for this lock becomes 1.
2. **Entering `secondMethod()`:** While still holding the lock from the first method, the thread calls `secondMethod()`.
3. **The Second Lock Call:** Inside `secondMethod()`, the thread calls `lock.lock()` again.
* Because this is a **Reentrant** lock, the JVM checks: "Does the current thread already own this lock?"
* The answer is **Yes**, so the thread is allowed to proceed immediately.
* The **hold count** now increases to 2.


4. **Unwinding the stack:**
* As `secondMethod()` finishes, its `finally` block calls `lock.unlock()`. The hold count drops back to 1. The lock is **not yet released** to other threads.
* As `firstMethod()` finishes, its `finally` block calls `lock.unlock()`. The hold count drops to 0, and the lock is now fully released.



---

### Key Components

| Component | Purpose |
| --- | --- |
| **`final ReentrantLock lock`** | Creates the lock object. The `final` keyword ensures the reference doesn't change, which is a best practice for thread safety. |
| **`lock.lock()`** | Acquires the lock. If another thread held it, the current thread would pause here. |
| **`try-finally` block** | **Crucial:** Always wrap lock logic in a `try` block and call `unlock()` in `finally`. This ensures the lock is released even if an exception occurs, preventing a permanent deadlock. |

### Why is this useful?

Without reentrancy, the code above would **deadlock**. The thread would be waiting at the start of `secondMethod()` for the lock to be released, but the lock can't be released until `secondMethod()` finishes. Reentrancy allows for much more flexible and modular code where synchronized methods can call each other freely.

