# Atomic variables

If `volatile` is a "light switch" (it’s either on or off, and everyone sees it), then **Atomic** classes are like a "smart thermostat"—they can read the current state, perform logic, and update the value all in one unbreakable step.

Here is a brief tutorial on how to use them effectively.

---

## 1. The Core Concept: CAS

Atomic classes don't use "locks" (which make threads wait in line). Instead, they use an optimistic strategy called **Compare-And-Swap (CAS)**.

1. It reads the value.
2. It calculates the new value.
3. Before saving, it asks the CPU: *"Is the value still what I read a moment ago?"*
4. If **yes**, it updates. If **no**, it retries.

---

## 2. Common Atomic Classes

All of these are found in the `java.util.concurrent.atomic` package:

* **`AtomicInteger` / `AtomicLong**`: For counters and sequence generators.
* **`AtomicBoolean`**: For flags that need "check-then-act" logic (e.g., "only do this if the flag was false, then set it to true").
* **`AtomicReference<T>`**: For updating an entire object reference atomically.

---

## 3. Essential Methods

Here are the methods you'll use 90% of the time:

| Method | Description | Equivalent to... |
| --- | --- | --- |
| `get()` | Reads the current value. | `return value;` |
| `set(newValue)` | Writes a new value. | `value = newValue;` |
| `incrementAndGet()` | Adds 1 and returns the result. | `++count;` (Thread-safe) |
| `getAndIncrement()` | Returns result then adds 1. | `count++;` (Thread-safe) |
| `compareAndSet(exp, update)` | Updates **only if** current == expected. | `if(v == e) v = u;` |

---

## 4. Code Example: The Safe Counter

In this example, even with 1,000 threads hitting the counter at once, the final total will be exactly 1,000. This would **fail** with a regular `volatile int`.

```java
import java.util.concurrent.atomic.AtomicInteger;

public class AtomicExample {
    // No need for 'volatile' here; AtomicInteger handles it!
    private final AtomicInteger counter = new AtomicInteger(0);

    public void increment() {
        // This is atomic: read, add, and write in one step
        counter.incrementAndGet(); 
    }

    public int getValue() {
        return counter.get();
    }

    public static void main(String[] args) throws InterruptedException {
        AtomicExample example = new AtomicExample();
        
        // Simulating 1000 concurrent increments
        for (int i = 0; i < 1000; i++) {
            new Thread(example::increment).start();
        }

        Thread.sleep(2000); // Wait for threads to finish
        System.out.println("Final Count: " + example.getValue()); // Will be 1000
    }
}

```

---

## When to use Atomic vs. Synchronized?

* **Use Atomic** for single variables (counters, flags, state transitions). It is much faster because it doesn't "block" or "suspend" threads.
* **Use Synchronized** when you need to update **multiple** variables together as a single unit (e.g., moving money from `Account A` to `Account B`).

