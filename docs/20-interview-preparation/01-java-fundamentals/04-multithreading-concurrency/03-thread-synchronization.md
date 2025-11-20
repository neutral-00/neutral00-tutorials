# Thread Synchronization in Java
Thread synchronization in Java is a mechanism that controls access to shared resources in a multi-threaded environment, ensuring that only one thread at a time can operate on a critical section of code or a shared resource.

## Why we need Thread Synchronization?
- Thread synchronization is crucial for maintaining data consistency in multi-threaded applications. 
- It helps prevent race conditions and ensures thread-safe access to shared resources.

## Race Conditions

A race condition occurs when multiple threads access shared resources simultaneously, potentially leading to unpredictable results:

```java
// Example of a race condition
public class BankAccount {
    private int balance = 0;
    
    public void deposit(int amount) {
        balance = balance + amount; // Not thread-safe!
    }
    
    public void withdraw(int amount) {
        balance = balance - amount; // Not thread-safe!
    }
}
```

## The `synchronized` Keyword

Java provides the `synchronized` keyword to prevent race conditions. It can be used in two ways:

### 1. Synchronized Methods

```java
public class BankAccount {
    private int balance = 0;
    
    public synchronized void deposit(int amount) {
        balance = balance + amount;
    }
    
    public synchronized void withdraw(int amount) {
        if (balance >= amount) {
            balance = balance - amount;
        }
    }
}
```

### 2. Synchronized Blocks

```java
public class BankAccount {
    private int balance = 0;
    private final Object lock = new Object(); // dedicated lock object
    
    public void deposit(int amount) {
        synchronized(lock) {
            balance = balance + amount;
        }
    }
    
    public void withdraw(int amount) {
        synchronized(lock) {
            if (balance >= amount) {
                balance = balance - amount;
            }
        }
    }
}
```

## The `volatile` Keyword

The `volatile` keyword ensures that a variable is read directly from main memory, not from thread-local cache:

```java
public class StatusChecker {
    private volatile boolean running = true;
    
    public void stop() {
        running = false;
    }
    
    public void run() {
        while(running) {
            // do work
        }
    }
}
```

Use `volatile` when:
- Variable is accessed by multiple threads
- Variable can be modified by one thread and read by others
- You don't need atomic operations

## Wait and Notify Mechanism

The `wait()`, `notify()`, and `notifyAll()` methods enable thread communication:

```java
public class MessageQueue {
    private String message;
    
    public synchronized void send(String message) {
        while(this.message != null) {
            try {
                wait(); // Release lock and wait
            } catch(InterruptedException e) {
                Thread.currentThread().interrupt();
            }
        }
        this.message = message;
        notify(); // Wake up waiting thread
    }
    
    public synchronized String receive() {
        while(message == null) {
            try {
                wait();
            } catch(InterruptedException e) {
                Thread.currentThread().interrupt();
            }
        }
        String result = message;
        message = null;
        notify();
        return result;

        
    }
}
```

## Lock Interface

Java provides the `Lock` interface for more flexible synchronization:

```java
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class BankAccount {
    private int balance = 0;
    private final Lock lock = new ReentrantLock();
    
    public void deposit(int amount) {
        lock.lock();
        try {
            balance += amount;
        } finally {
            lock.unlock(); // Always release in finally block
        }
    }
}
```

### ReadWriteLock

For scenarios with many reads and few writes:

```java
import java.util.concurrent.locks.ReadWriteLock;
import java.util.concurrent.locks.ReentrantReadWriteLock;

public class CacheData {
    private Map<String, String> cache = new HashMap<>();
    private ReadWriteLock lock = new ReentrantReadWriteLock();
    
    public String read(String key) {
        lock.readLock().lock();
        try {
            return cache.get(key);
        } finally {
            lock.readLock().unlock();
        }
    }
    
    public void write(String key, String value) {
        lock.writeLock().lock();
        try {
            cache.put(key, value);
        } finally {
            lock.writeLock().unlock();
        }
    }
}
```

## Atomic Classes

Java provides atomic classes for thread-safe operations:

```java
import java.util.concurrent.atomic.AtomicInteger;

public class Counter {
    private AtomicInteger count = new AtomicInteger(0);
    
    public void increment() {
        count.incrementAndGet(); // Atomic operation
    }
    
    public int getCount() {
        return count.get();
    }
}
```

## Best Practices

1. **Keep Synchronized Blocks Small**
   ```java
   // Good: Minimal synchronized section
   public void process(Data data) {
       // Do non-synchronized work here
       synchronized(lock) {
           // Only synchronize critical section
       }
       // Do more non-synchronized work here
   }
   ```

2. **Avoid Nested Synchronization**
   ```java
   // Bad: Potential deadlock
   synchronized(lockA) {
       synchronized(lockB) {
           // ...
       }
   }
   
   // Good: Use composite locks or higher-level concurrency utilities
   ```

3. **Use Higher-Level Concurrency Utilities**
   ```java
   // Instead of manual synchronization
   private BlockingQueue<Task> queue = new ArrayBlockingQueue<>(100);
   private ConcurrentHashMap<String, User> users = new ConcurrentHashMap<>();
   ```

4. **Prefer Lock Interface Over Synchronized**
   - More flexible
   - Supports fairness
   - Allows try-lock operations
   - Provides separate read/write locks

5. **Document Thread Safety**
   ```java
   /**
    * This class is thread-safe.
    * All public methods are synchronized on the instance.
    */
   public class ThreadSafeClass {
       // ...
   }
   ```

## Common Issues

1. **Deadlock**
   ```java
   // Potential deadlock
   public void method1() {
       synchronized(resourceA) {
           synchronized(resourceB) {
               // ...
           }
       }
   }
   
   public void method2() {
       synchronized(resourceB) {
           synchronized(resourceA) {
               // ...
           }
       }
   }
   ```

2. **Starvation**
   ```java
   // Use fair locks to prevent starvation
   private final Lock lock = new ReentrantLock(true); // fair lock
   ```

3. **Livelock**
   ```java
   // Avoid overly complex retry logic
   while(true) {
       if(tryLock()) {
           // do work
           break;
       }
       // Add random delay to prevent livelock
       Thread.sleep(new Random().nextInt(100));
   }
   ```