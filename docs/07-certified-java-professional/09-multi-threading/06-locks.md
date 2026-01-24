# Locks

When we use the `synchronized` keyword in the a method or block and a thread executes that block,
JVM applies lock to that block so that other threads can't acceess it.

There are 2 types of locks:

1. Intrinsic Lock : 
    - They are built into every object in Java.
    - `sysnchronized` keyworkd uses these locks.
    - They are automatic and not visible.

2. Explicit Lock
    - They are advanced locks can created using the Lock interface from `java.util.concurrent.lock` package.
    - Here you control when to lock or unlock.

Suppose, you have a `BankAccount` class as follows:

```java

package org.lousing.multithreading;

import java.util.concurrent.TimeUnit;
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReentrantLock;

public class BankAccount {
    private int balance = 100;

    private final Lock lock = new ReentrantLock();

    public void withdraw(int amount) {
        var threadName = Thread.currentThread().getName();
        System.out.println(threadName + " attempting to withdraw amount : " + amount);
        try {
            if (lock.tryLock(1000, TimeUnit.MILLISECONDS)) {
                if (balance >= amount) {
                    System.out.println(threadName + " proceeding with withdrawal");
                    try {
                        Thread.sleep(5000); // simulating time taking operation
                        balance -= amount;
                        System.out.println(threadName + " completed withdrawal, remaining " + balance);
                    } catch (InterruptedException e) {
                        throw new RuntimeException(e);
                    } finally {
                        lock.unlock();
                    }
                } else {
                    System.out.println(threadName + " insufficient balance");
                }
            } else {
                System.out.println(threadName + " could not acquire the lock. will try again later...");
            }
        } catch (InterruptedException e) {
            throw new RuntimeException(e);
        }
    }
}
```

Let's run the withdraw method by two threads. Predict whether both can succeed.

```java

package org.lousing.multithreading;

public class LockExample {
    public static void showDemo() {
        BankAccount bankAccount = new BankAccount();
        Runnable task = new Runnable() {
            @Override
            public void run() {
                bankAccount.withdraw(50);
            }
        };
        Thread t1 = new Thread(task,"T1");
        Thread t2 = new Thread(task,"T2");
        t1.start();
        t2.start();
    }
}
```

Result: only one of them succeeds.

Reason, one thread can wait for 1 second. But the code to withdraw balance is taking 3 seconds.

Also note that we have used `ReentrantLock`
