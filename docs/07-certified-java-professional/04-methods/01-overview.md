# Method Overview

Methods are blocks of code that perform a specific task.

A method follows the folling syntax
```
<access modifier> <return type> <method name> (<parameters>) {
    // body
}
```


```java

package org.lousing.methods;

public class Calculator {

    public static int sum(int a, int b) {
        System.out.println("Integer a + b = " + (a + b));
        return  a + b;
    }

}
```
