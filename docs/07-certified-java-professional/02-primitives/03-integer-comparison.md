# Integer Comparison

```java
public static void demoIntegerDoubleEquals() {
        System.out.println("\n------------------Integer Comparison--------------------");
        
        Integer a = 100;
        Integer b = 100;

        System.out.println("a == b is " + (a == b)); // true (cached)
        System.out.println("a.equals(b) ia " + a.equals(b)); // true

        Integer x = 10; // basically translates to Integer x = Integer.valueOf(10)
        Integer y = Integer.valueOf(10);

        System.out.println("x == y is " + (x == y)); // true
        System.out.println("x.equals(y) is " + x.equals(y)); // true

        Integer i = 128; // Note: Java caches Integer Objects between -128 to 127
        Integer j = new Integer(128); // deprecated since Java 9 - use Integer.valueOf() instead

        System.out.println("i == j is " + (i == j)); // false
        System.out.println("i.equals(j) = " + i.equals(j)); // true

        Integer k = 128;
        Integer l = 128;

        System.out.println("k==l is " + (k == l)); // false
        System.out.println("k.equals(l) is " + (k.equals(l))); // true

        /*
         * 🔥 Important things to remember
         * ➡️ Integer a = 100 basically translates to Integer a = Integer.valueOf(100)
         * ➡️ Java caches Integer objects between -128 and 127. Outside this range new objects are created
         * ➡️ new Integer(x) is deprecated from Java 9+
         * ➡️ all objects have an equals method to compare values. By default, it compares references.
         * ➡️ override it to compare using field(s) defined in the object
         * */
}
```
