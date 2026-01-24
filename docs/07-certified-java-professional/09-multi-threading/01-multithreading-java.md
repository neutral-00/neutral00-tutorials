# Multithreading In Java

It is the execution of two or more threads to maximise cpu utilization. \
`java.lang` package contains the necessary tools for multithreading.

In multi-core cpu, JVM can distribute threads across multiple cores.
This is will result in true parallel execution.

## How to create a thread
There are 2 ways:
1. `java.lang.Thread` class
2. `java.lang.Runnable` interface


When a java program is run, JVM looks for a method named main and that is executed as the main thread.


So inside the main method, you can run `Thread.currentThread().getName()` to get the thread name.
You will get `main`.


```java
// extending Thread
package org.lousing.multithreading;

import java.util.stream.IntStream;

public class ThreadExample extends Thread {

    @Override
    public void run() {
        IntStream.range(200,500).forEach(n-> System.out.println("Extending the Thread class " + n));
    }
}


// implementing Runnable
package org.lousing.multithreading;

import java.util.stream.IntStream;

public class RunnableExample implements Runnable {
    @Override
    public void run() {
        IntStream.range(200, 500).forEach(n -> System.out.println("Implementing the Runnable Interface " + n));
    }
}

// let's run them

package org.lousing.multithreading;

public class ThreadController {
    public static void showDemo() {
        ThreadExample t = new ThreadExample();
        RunnableExample runnableExample = new RunnableExample();
        Thread r = new Thread(runnableExample);
        t.start();
        r.start();
    }
}
```


## Thread vs Runnable
- A class already extends another class then we cannot extend Thread class as java wont allow it.
- In this case, Runnable Interface comes into the rescue.


