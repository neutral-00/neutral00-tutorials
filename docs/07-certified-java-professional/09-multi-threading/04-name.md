# Name a thread


```java

package org.lousing.multithreading;

public class NamedThread extends Thread{

    public NamedThread(String name) {
        super(name);
    }

    public void run() {
        System.out.println("I am a named thread");
        System.out.println("My name is " + Thread.currentThread().getName());
    }
}
```



