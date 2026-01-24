# Filter Operation

The `filter` operation in Streams API is used to select elements from a stream that matched a given predicate. \
Predicate is a boolean-valued function. \
Filter is an intermediate operation.
It is defined in the `Stream` interface as follow:

```java
Stream<T> filter(Predicate<? super T> predicate) 
```
- `filter` method takes `Predicate` as an argument and return a new stream consisting of elements that matches the predicate.
- Note that the original stream remains unchanged.

Example: Get employees with salary greater than 50k.
```java

```
