# Synchronization

The `synchronized` keyword is used in a method definition or a block to make sure only one thread aaccess the block of codes at a time.

```java

package org.lousing.multithreading;

public class Counter {

    private int count = 0;

    public synchronized void increment() {
        count++;
    }

    public int getCount() {
        return count;
    }
}
```

Or

```java

package org.lousing.multithreading;

public class Counter {

    private int count = 0;

    public void increment() {
        synchronized (this) {
            count++;
        }
    }

    public int getCount() {
        return count;
    }
}
```

## What are the advantae and disadvantage of synchronization using synchronized keyword?

In Java, the `synchronized` keyword is the simplest and most common way to achieve **thread safety**. It ensures that only one thread can execute a specific block of code at a time, preventing "race conditions" where multiple threads try to modify the same data simultaneously.

---

### Advantages of Using `synchronized`

* **Simplicity and Readability:** It is built directly into the Java language. You don’t need to manually create, lock, or unlock objects (like you would with `ReentrantLock`). This makes the code easier to write and maintain.
* **Automatic Release:** If an exception occurs within a `synchronized` block, the JVM automatically releases the lock. This prevents "deadlocks" that would occur if you forgot to unlock a manual lock in a `finally` block.
* **Memory Visibility:** Beyond just locking, it guarantees that changes made by one thread to a shared variable are visible to all other threads once the lock is released.
* **Reentrancy:** The `synchronized` keyword is **reentrant**. This means if a thread already holds a lock, it can enter other synchronized blocks that use the same lock without getting stuck.

---

### Disadvantages of Using `synchronized`

* **Performance Overhead:** Acquiring and releasing locks takes time. If a block of code is synchronized but doesn't actually need to be, it can slow down your application unnecessarily.
* **Lack of Flexibility:** * You cannot check if a lock is available without waiting (no `tryLock()` capability).
* You cannot interrupt a thread that is waiting to enter a `synchronized` block.
* Locks must be acquired and released in the same method/block (structured locking).


* **Coarse-Grained Locking:** It is often difficult to implement "read-write" separation. With `synchronized`, if one thread is reading, no other thread can read at the same time, which can be inefficient for read-heavy applications.
* **Risk of Deadlock:** If not used carefully—such as when two threads are waiting for locks held by each other—it can lead to a complete system hang.

---

### Summary Table

| Feature | `synchronized` Keyword |
| --- | --- |
| **Ease of Use** | High (Built-in) |
| **Safety** | High (Auto-release on exception) |
| **Performance** | Moderate (Heavier than atomic variables) |
| **Control** | Low (Wait is unconditional) |

Would you like me to show you a code example comparing a **synchronized method** versus a **synchronized block** to see which is better for performance?
