# `type` vs `interface` in TypeScript

Both `type` and `interface` are used to describe the **shape of data** in TypeScript.
They are similar in many ways, but they have **important conceptual and practical differences**.

---

## The Big Picture

| Feature              | `type`            | `interface`   |
| -------------------- | ----------------- | ------------- |
| Object shapes        | ✅                 | ✅             |
| Union types          | ✅                 | ❌             |
| Intersection types   | ✅                 | ❌             |
| Declaration merging  | ❌                 | ✅             |
| Implements (classes) | ✅                 | ✅             |
| Extends              | Via intersections | Via `extends` |
| Preferred for APIs   | ⚠️                | ✅             |

---

## Interface

### What It Is

> An `interface` describes the **shape of an object** and is designed to be **extendable**.

---

### Example

```ts
interface Student {
  id: number;
  name: string;
  email: string;
}
```

Usage:

```ts
const student: Student = {
  id: 1,
  name: "Robin",
  email: "robin@example.com",
};
```

---

### Extending Interfaces

```ts
interface Student {
  id: number;
  name: string;
}

interface StudentWithAttendance extends Student {
  attendance: number;
}
```

✔️ Clean inheritance
✔️ Readable hierarchies

---

### Declaration Merging (Interface Only)

```ts
interface Student {
  age: number;
}

interface Student {
  grade: string;
}
```

TypeScript merges them:

```ts
interface Student {
  age: number;
  grade: string;
}
```

📌 This is **intentional** and commonly used in:

* Library augmentation
* Framework typings

---

## Type Alias (`type`)

### What It Is

> A `type` is an **alias** for any TypeScript type — not just objects.

---

### Example

```ts
type Student = {
  id: number;
  name: string;
  email: string;
};
```

---

### Where `type` Shines

#### Union Types

```ts
type Status = "loading" | "success" | "error";
```

Interfaces **cannot** do this.

---

#### Intersection Types

```ts
type Timestamped = {
  createdAt: Date;
};

type StudentWithMeta = Student & Timestamped;
```

---

#### Non-Object Types

```ts
type ID = string | number;
```

---

## Implementing with Classes

Both work equally well:

```ts
interface Person {
  name: string;
}

class User implements Person {
  name = "Robin";
}
```

```ts
type Person = {
  name: string;
};

class User implements Person {
  name = "Robin";
}
```

✔️ No difference here

---

## Key Differences (Deep Dive)

### 1️⃣ Declaration Merging

|                       | `interface` | `type` |
| --------------------- | ----------- | ------ |
| Multiple declarations | ✅           | ❌      |

```ts
interface Config {
  apiUrl: string;
}

interface Config {
  timeout: number;
}
```

This is impossible with `type`.

---

### 2️⃣ Extending / Combining

```ts
interface A {
  a: number;
}

interface B extends A {
  b: number;
}
```

vs

```ts
type A = {
  a: number;
};

type B = A & {
  b: number;
};
```

Both are valid, but:

* Interfaces feel more **OOP-style**
* Types feel more **functional/compositional**

---

### 3️⃣ Error Messages & Readability

Interfaces often produce **cleaner error messages** for large object types.

This matters in public APIs.

---

## When to Use What (Rule of Thumb)

### Prefer `interface` when:

* Defining object shapes
* Designing public APIs
* Expecting extension or augmentation
* Working with classes

---

### Prefer `type` when:

* Working with unions or intersections
* Defining aliases
* Creating complex composed types
* Modeling non-object data

---

## Common Misconceptions

### ❌ “Interfaces are deprecated”

False. They are actively recommended.

### ❌ “Type is more modern”

Not true — they serve different purposes.

---

## Recommended Team Guideline

> **Use `interface` for object shapes,
> use `type` for everything else.**

This guideline works well in **most real-world codebases**.

---

## Summary

* Both `type` and `interface` describe shapes
* Interfaces are extendable and mergeable
* Types are more flexible and expressive
* They complement each other — not competitors

---

## Credit

> Official docs
> [https://www.typescriptlang.org/docs/handbook/2/objects.html](https://www.typescriptlang.org/docs/handbook/2/objects.html)
> [https://www.typescriptlang.org/docs/handbook/2/everyday-types.html](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html)

---

### Teaching Tip

Teach this **after**:

* `Record`
* `Pick` / `Omit`
* `unknown` / `never`

At this point, learners understand *why* these distinctions matter.

---

