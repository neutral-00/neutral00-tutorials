# Prevent Object From Being Cloned

## Actual Question Metadata

- company: FIS GLOBAL
- role: Java Senior Developer With SRE
- Date: 2025-12-10

To prevent a Java object from being cloned, override the `clone()` method from `Object` and throw `CloneNotSupportedException`.[2][3]

## Implementation

```java
public class ImmutableObject implements Cloneable {
    // class fields and constructor

    @Override
    protected Object clone() throws CloneNotSupportedException {
        throw new CloneNotSupportedException("Cloning is not supported for this object");
    }
}
```

Any attempt to call `obj.clone()` now fails with the exception, blocking shallow or deep copies via cloning.[1][2]

You're on the right track 👍. Overriding `clone()` to throw `CloneNotSupportedException` is indeed the standard way to block cloning. A couple of refinements and alternatives you might want to note for completeness:

---

## Additional Points

- **No need to implement `Cloneable`**
  - If your goal is to _prevent_ cloning, you don’t need to implement the `Cloneable` interface at all.
  - By default, `Object.clone()` throws `CloneNotSupportedException` unless the class implements `Cloneable`.
  - So simply omitting `Cloneable` already blocks cloning attempts.

- **Explicit override for clarity**
  - Overriding `clone()` and throwing `CloneNotSupportedException` (as you did) makes the intent explicit to anyone reading the code.
  - This is often preferred in immutable or security-sensitive classes.

- **Marking the class `final`**
  - If immutability is your goal, consider declaring the class `final`.
  - Otherwise, a subclass could override `clone()` and re-enable cloning.

- **Alternative defensive approach**
  - Instead of throwing, you could override `clone()` to return `this`.
  - This enforces immutability by ensuring all "copies" are just references to the same object.
  - Example:
    ```java
    @Override
    protected Object clone() {
        return this;
    }
    ```

- **Copy constructors or factory methods**
  - If you want controlled duplication, provide a copy constructor or a static factory method instead of relying on `clone()`.
  - This is the modern best practice in Java, since `clone()` is widely considered flawed and outdated.

---

## Refined Example

```java
public final class SomeClass {
    // class fields and constructor

    @Override
    protected final Object clone() throws CloneNotSupportedException {
        throw new CloneNotSupportedException("Cloning is not supported for SomeClass");
    }
}
```

This version:

- Removes `Cloneable` (since it’s unnecessary).
- Marks the class `final` to prevent subclass circumvention.
- Keeps the explicit override for clarity.

---

👉 So the complete picture is:

- Don’t implement `Cloneable` if you don’t want cloning.
- Optionally override `clone()` to throw for clarity.
- Consider `final` for immutability.
- Prefer copy constructors or factories for controlled duplication.
