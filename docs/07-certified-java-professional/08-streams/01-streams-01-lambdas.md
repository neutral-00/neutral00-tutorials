# Lambdas

A lambda is essentially a shortcut for writing a method. \
It is a way to write code that cab be passed around as data. \
It provides a concise way to represent one method interface using an expression. \
Lambda expression are used implement functional interfaces.


The most common syntax is `(parameter) -> expression` or `(parameters) -> { statments; }`

Lambdas integrate well with the Java Collections Framework, allowing for more expressive and concise operations on collections.

They are often used with the Stream API to perform operations on collections.

## Lambda way to iterate an arrayList
```java
var flowers = new ArrayList<String>();
flowers.add("Mary Gold");
flowers.add("Rose");
flowers.forEach(f-> System.out.println(f));
```


## Functional Interface

A funtional interface is simply an interface that has exactly one abstract method(a method with no body).
So it is like a contract for a single behavior. \
Have a look at one of the in-built functional interface provided by Java:
```java
@FunctionalInterface
public interface Predicate<T> {
  boolean test(T t); // single abstract method
}
```
Below is how you can write a lambda expression to implement this interface and override the test method

```java
Predicate<String> longFlowerNameCheck = f -> s.length > 10;
```
Here Java uses Type Inference and says like, Predicate interface has only one abstract method let me map the lambda expression to that method.

That's why single abstract method is important.

You can reuse the following built-in functional interfaces from the `java.util.function` package.
1. `Predicate<T>` with the method `test` that returns a boolean.
2. `Function<T,R>` with the method `R apply(T t)`
3. `Consumer<T>` with the method `void accept(T t)`
4. `Supplier<T>` with the method `T get()`


## Method References
- They are a shorthand to lamba expressions that refer to existing methods.

Example
```java

```
