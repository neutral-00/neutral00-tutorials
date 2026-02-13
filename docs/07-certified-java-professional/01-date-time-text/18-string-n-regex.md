# Regex

Let's solve one problem using regular expression in Java.

## Problem Description

Write a program that prints array of words entered by user without any spaces or punctuation marks.

```java

import java.util.Arrays;
import java.util.Scanner;

public class SplitWords {
	
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		System.out.print("Please, enter any text: ");
		String userInput = sc.nextLine();
		System.out.print("You entered these words: ");
		System.out.println(Arrays.toString(userInput.split("[^\\p{L}\\p{N}]+"
)));
	}

}

```


### The Unicode-friendly regex

```java
"[^\\p{L}\\p{N}]+"
```

Let’s decode it piece by piece.

---

## 1. `\p{...}` — Unicode character classes

In regex, `\p{X}` means:

> “Any character that belongs to Unicode category **X**”

These categories are defined by the Unicode standard.

---

## 2. `\p{L}` — Letters

```txt
\p{L}
```

Matches **any letter**, from any language:

* English: `a b c`
* Accented: `é ñ ü`
* Greek: `α β γ`
* Cyrillic: `Ж Д`
* Asian scripts: `中 日 本`

So this is much more powerful than `[A-Za-z]`.

---

## 3. `\p{N}` — Numbers

```txt
\p{N}
```

Matches **any numeric character**:

* `0–9`
* Arabic-Indic digits
* Roman numerals
* Other Unicode number forms

Again, broader than `[0-9]`.

---

## 4. Putting them together

```java
\\p{L}\\p{N}
```

Means:

> letters **or** numbers (from *any* language)

---

## 5. The `^` inside `[]` — Negation

```java
[^\\p{L}\\p{N}]
```

Means:

> anything that is **NOT** a letter or number

This includes:

* spaces
* punctuation
* symbols
* emojis

---

## 6. The `+` quantifier

```java
+
```

Means:

> one or more consecutive characters

So multiple spaces or punctuation marks are treated as **one split point**.

---

## 7. Final meaning (plain English)

```java
"[^\\p{L}\\p{N}]+"
```

➡️ “Split the string **wherever one or more non-letter and non-number characters occur**.”

---

## Example

Input:

```txt
¡Hola! ¿Cómo estás? 你好，世界 🌍
```

Output:

```txt
[Hola, Cómo, estás, 你好, 世界]
```

Your original ASCII-only regex would have lost most of that.

---

## Why this matters

Using Unicode classes:

* makes your code **international-friendly**
* avoids subtle bugs with accented characters
* is best practice for user-entered text

---

### Quick mental shortcut

* `\p{L}` → letters
* `\p{N}` → numbers
* `[^...]` → “everything except”
* `+` → group consecutive separators

