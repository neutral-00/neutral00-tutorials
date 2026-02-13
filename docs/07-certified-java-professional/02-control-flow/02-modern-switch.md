# Modern `switch` Expressions

## 1. Why Was `switch` Improved?

### Old `switch` problems

* Verbose
* Easy to forget `break`
* Fall-through bugs
* Could not **return a value** cleanly

```java
int result;
switch (day) {
    case 1:
        result = 10;
        break;
    case 2:
        result = 20;
        break;
    default:
        result = 0;
}
```

---

## 2. Switch Expressions (Java 14+)

Modern `switch` can now **return a value**, just like an expression.

```java
int result = switch (day) {
    case 1 -> 10;
    case 2 -> 20;
    default -> 0;
};
```

✔ No `break`
✔ More readable
✔ Safer

---

## 3. Arrow (`->`) Syntax

The arrow syntax replaces `:` and eliminates fall-through.

```java
switch (status) {
    case "OPEN" -> System.out.println("Open");
    case "CLOSED" -> System.out.println("Closed");
}
```

Each case is **isolated by default**.

---

## 4. Returning Values from Switch

### Simple value return

```java
String dayType = switch (day) {
    case 1, 7 -> "Weekend";
    case 2, 3, 4, 5, 6 -> "Weekday";
    default -> "Invalid";
};
```
ℹ️ Info ⭐
- Java switch does not support ranges. Use comma-separated constants or enums
---

## 5. Multiple Case Labels (Comma-Separated)

Old way:

```java
case 1:
case 7:
```

New way:

```java
case 1, 7 -> "Weekend";
```

Much cleaner.

---

## 6. Block Cases and `yield`

When logic is more complex, use a **block** with `yield`.

```java
String grade = switch (score) {
    case 90, 100 -> {
        System.out.println("Excellent");
        yield "A";
    }
    case 75, 80, 85 -> "B";
    default -> "C";
};
```

### Why `yield`?

* Returns a value from a switch block
* Replaces `break value`

---

## 7. Exhaustiveness (Compiler Safety)

Switch expressions **must cover all cases**.

```java
enum Status { OPEN, CLOSED }

Status s = Status.OPEN;

String msg = switch (s) {
    case OPEN -> "Open";
    case CLOSED -> "Closed";
};
```

✔ No `default` needed
✔ Compiler ensures safety

---

## 8. Switching on More Types

Modern switch supports:

* `int`, `char`
* `String`
* `enum`
* Wrapper types (`Integer`)
* (Preview / newer Java) pattern matching

```java
String result = switch (input) {
    case "yes", "y" -> "Accepted";
    case "no", "n" -> "Rejected";
    default -> "Unknown";
};
```

---

## 9. Switch Statement vs Switch Expression

| Feature           | Old Switch | Modern Switch |
| ----------------- | ---------- | ------------- |
| Returns value     | ❌          | ✅             |
| Fall-through safe | ❌          | ✅             |
| Requires break    | ✅          | ❌             |
| Expression-style  | ❌          | ✅             |

---

## 10. When NOT to Use Switch Expressions

* When logic is **very large**
* When side effects dominate
* When polymorphism fits better (OO design)

---

## 11. Best Practices ⭐

* Prefer **expression form** when assigning values
* Avoid `default` when switching on `enum` (let compiler help)
* Use `yield` only for multi-line logic
* Keep cases small and readable

---

## 12. Interview One-Liner

> Modern switch expressions in Java allow switch to return values, remove fall-through bugs, and improve readability using arrow syntax and `yield`.

---

## 13. Migration Tip

Old:

```java
switch (x) {
    case 1: return "A";
    case 2: return "B";
    default: return "C";
}
```

New:

```java
return switch (x) {
    case 1 -> "A";
    case 2 -> "B";
    default -> "C";
};
```

---

