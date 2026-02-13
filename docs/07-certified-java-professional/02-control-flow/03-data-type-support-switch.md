# Data Types Supported In Switch


## 1️⃣ Primitive Types Support (New Switch)

### ✅ Supported (Same as Old Switch)

| Primitive Type | Supported | Notes             |
| -------------- | --------- | ----------------- |
| `byte`         | ✅         | Promoted to `int` |
| `short`        | ✅         | Promoted to `int` |
| `char`         | ✅         | Integral          |
| `int`          | ✅         | Native            |

---

### ❌ Still NOT Supported

| Primitive Type | Supported | Why                         |
| -------------- | --------- | --------------------------- |
| `long`         | ❌         | Still no jump-table support |
| `float`        | ❌         | Precision & NaN issues      |
| `double`       | ❌         | Precision & NaN issues      |
| `boolean`      | ❌         | Binary condition → `if`     |

So this is **still invalid**, even in modern switch:

```java
long l = 10;

switch (l) {   // ❌ compile-time error
    case 10 -> "Ten";
}
```

---

## 2️⃣ Wrapper Classes (New Switch)

### ✅ Supported (Auto-Unboxing)

| Wrapper     | Supported |
| ----------- | --------- |
| `Byte`      |           |
| `Short`     |           |
| `Character` |           |
| `Integer`   |           |

```java
Integer x = 2;

String result = switch (x) {
    case 1 -> "One";
    case 2 -> "Two";
    default -> "Other";
};
```

---

### ❌ Still NOT Supported

* `Long`
* `Float`
* `Double`
* `Boolean`

Same as before.

---

## 3️⃣ `String` Support

Still supported (since Java 7), now with **expression syntax**:

```java
String result = switch (cmd) {
    case "start" -> "Starting";
    case "stop" -> "Stopping";
    default -> "Unknown";
};
```

---

## 4️⃣ `enum` Support (Best Use Case)

Modern switch shines with enums:

```java
enum Day { MON, TUE, WED, THU, FRI, SAT, SUN }

String type = switch (day) {
    case SAT, SUN -> "Weekend";
    default -> "Weekday";
};
```

✔ Exhaustiveness checking
✔ No `default` needed
✔ Compile-time safety

---

## 5️⃣ Pattern Matching (New Capability 🚀)

This is where **new switch really differs**.

### Switch with patterns (Java 21+)

```java
Object obj = "Hello";

String result = switch (obj) {
    case Integer i -> "Number: " + i;
    case String s -> "Text: " + s;
    case null -> "Null";
    default -> "Unknown";
};
```

✔ Works with **Object types**
✔ Type-safe
✔ No casting

> ⚠️ This is **not about primitive types**, but it greatly expands switch power.

---

## 6️⃣ Can New Switch Do Ranges?

❌ **Still no numeric ranges**

```java
case 1..5 -> "Low"; // ❌ not allowed
```

Use:

* comma-separated constants
* `if`
* enums
* pattern guards (future-style logic)

---

## 7️⃣ Summary Table ⭐

| Type                           | Old Switch | New Switch |
| ------------------------------ | ---------- | ---------- |
| `byte`, `short`, `char`, `int` | ✅          | ✅          |
| `long`                         | ❌          | ❌          |
| `float`, `double`              | ❌          | ❌          |
| `boolean`                      | ❌          | ❌          |
| Wrapper (`Integer`, etc.)      | ✅          | ✅          |
| `String`                       | ✅          | ✅          |
| `enum`                         | ✅          | ✅          |
| Object patterns                | ❌          | ✅          |

---

## 8️⃣ Interview One-Liner

> The new Java switch improves syntax, safety, and expressiveness, but it keeps the same primitive type restrictions as the old switch; its real power comes from expressions, enums, and pattern matching.

---

## 9️⃣ Rule of Thumb

* Use **switch** for discrete values
* Use **if** for ranges
* Use **enums** for domain concepts
* Use **pattern matching switch** for heterogeneous objects

---

If you want, next we can:

* Refactor `if-else` chains into **modern switch**
* Compare **switch vs polymorphism**
* Deep dive into **pattern guards**
* Show **real interview traps**

Just say where to go next 🚀
