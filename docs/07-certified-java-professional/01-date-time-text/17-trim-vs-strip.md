# String - trim vs strip

## One liner: trim removes trailing ascii whitespaces while strip removes ascii + unicode whitespaces.

They’re *similar*, but **not the same** — and the difference matters once you leave plain ASCII.

### `trim()`

* Old-school (been around forever)
* Removes **leading and trailing characters ≤ U+0020**

  * space
  * tab `\t`
  * newline `\n`
  * carriage return `\r`
* **Does NOT handle all Unicode whitespace**

```java
" hello ".trim();   // ← may NOT remove non-breaking space
```

---

### `strip()` (Java 11+)

* Unicode-aware
* Removes **all Unicode whitespace**
* Uses `Character.isWhitespace()`

```java
" hello ".strip();  // ← removes it correctly
```

This includes:

* non-breaking spaces
* em spaces
* ideographic spaces
* etc.

---

### Side-by-side

```java
String s = "\u2003hello\u2003"; // em space

System.out.println(s.trim().length());  // > 5  (spaces still there)
System.out.println(s.strip().length()); // 5    (spaces removed)
```

---

### Quick comparison

| Method    | Java version | Whitespace handling |
| --------- | ------------ | ------------------- |
| `trim()`  | Java 1.0     | ASCII only          |
| `strip()` | Java 11      | Unicode-aware       |

---

### Bonus: left/right only

Java 11 also added:

```java
stripLeading();
stripTrailing();
```

---

### Which should you use?

* **Modern Java (11+)** → `strip()` ✅
* **Legacy code / Java 8** → `trim()` (but be aware of limitations)
* **User input / international text** → `strip()` absolutely

So yeah — they *often* look the same in simple cases, but `strip()` is the safer, modern choice 👍
