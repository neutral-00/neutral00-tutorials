# Method Reference

Method references are a shorthand notation of lambda expressions to call a method. \
They use the `::` operator.


## Types
1. Reference to static method
2. Reference to an instance method


```java

package org.lousing.multithreading;

public class MethodReferenceExample {

    public static void showDemo() {
        Thread thread = new Thread(MethodReferenceExample::printMessage);
        thread.run();
    }

    public static void printMessage() {
        System.out.println("Hi from printMessage method");
    }
}
```
