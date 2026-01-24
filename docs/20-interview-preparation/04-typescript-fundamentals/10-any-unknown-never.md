# `any`, `unknown`, and `never` in TypeScript

`any`, `unknown`, and `never` are **special types** in TypeScript.
They represent **very different levels of safety and intent**.

Understanding them properly is key to writing **correct and maintainable** TypeScript.

---

## Overview (Big Picture)

| Type      | Meaning                       | Safety   |
| --------- | ----------------------------- | -------- |
| `any`     | “I don’t care about the type” | ❌ Unsafe |
| `unknown` | “I don’t know the type yet”   | ✅ Safe   |
| `never`   | “This should never happen”    | ✅ Safe   |

---

## `any`

### What It Means

> `any` turns off TypeScript’s type checking.

You can:

* Assign anything to it
* Access any property
* Call it like a function

TypeScript will **not** help you.

---

### Example

```ts
let value: any;

value = 10;
value = "hello";
value = { x: 1 };

value.toUpperCase(); // No error at compile time
```

❌ This may crash at runtime.

---

### When (Rarely) to Use `any`

* Migrating legacy JavaScript
* Temporary escape hatch
* Quick prototyping (with intent to remove)

📌 **Rule**:
If you reach for `any`, ask yourself:

> “Should this be `unknown` instead?”

---

## `unknown`

### What It Means

> `unknown` represents a value whose type is not known **yet**.

Unlike `any`, TypeScript **forces you to check** before using it.

---

### Example

```ts
let value: unknown;

value = "hello";
value = 42;
```

❌ Not allowed:

```ts
value.toUpperCase(); // Error
```

---

### Narrowing `unknown`

You must **prove the type** first.

```ts
if (typeof value === "string") {
  value.toUpperCase(); // OK
}
```

Or with functions:

```ts
function handle(input: unknown) {
  if (typeof input === "number") {
    console.log(input * 2);
  }
}
```

✔️ Safe
✔️ Explicit
✔️ Encourages defensive programming

---

### `unknown` vs `any`

| Feature                   | any   | unknown |
| ------------------------- | ----- | ------- |
| Type checking             | ❌ Off | ✅ On    |
| Property access           | ✅     | ❌       |
| Assignment to other types | ✅     | ❌       |
| Preferred?                | ❌     | ✅       |

👉 **Prefer `unknown` for external data** (APIs, user input).

---

## `never`

### What It Means

> `never` represents values that **never occur**.

A function returning `never`:

* Never returns
* Always throws or loops forever

---

### Example: Function That Throws

```ts
function throwError(message: string): never {
  throw new Error(message);
}
```

---

### Example: Infinite Loop

```ts
function forever(): never {
  while (true) {}
}
```

---

## `never` in Exhaustive Checks (Very Important)

This is where `never` really shines.

```ts
type Shape =
  | { kind: "circle"; radius: number }
  | { kind: "square"; size: number };

function area(shape: Shape) {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "square":
      return shape.size ** 2;
    default:
      const _exhaustive: never = shape;
      return _exhaustive;
  }
}
```

✔️ If a new shape is added
✔️ Compiler forces you to update this code

This is **professional-grade TypeScript**.

---

## How `never` Differs from `void`

| Type    | Meaning         |
| ------- | --------------- |
| `void`  | Returns nothing |
| `never` | Never returns   |

```ts
function log(msg: string): void {
  console.log(msg);
}

function fail(): never {
  throw new Error("fail");
}
```

---

## Mental Model (Very Important)

* `any` → **opt out**
* `unknown` → **verify first**
* `never` → **impossible case**

---

## Common Mistakes

### ❌ Overusing `any`

```ts
function parse(data: any) {
  return data.value;
}
```

### ✅ Use `unknown`

```ts
function parse(data: unknown) {
  if (
    typeof data === "object" &&
    data !== null &&
    "value" in data
  ) {
    return (data as { value: string }).value;
  }
}
```

---

## Summary

* Avoid `any` whenever possible
* Use `unknown` for untrusted input
* Use `never` for:

  * Exhaustive checks
  * Impossible states
  * Functions that never return

---

## Credit

> Official docs
> [https://www.typescriptlang.org/docs/handbook/2/narrowing.html](https://www.typescriptlang.org/docs/handbook/2/narrowing.html)
> [https://www.typescriptlang.org/docs/handbook/basic-types.html](https://www.typescriptlang.org/docs/handbook/basic-types.html)

---

### Teaching Recommendation

Teach these **together**, in this order:

1. `any` (what *not* to do)
2. `unknown` (the safe alternative)
3. `never` (advanced correctness)

This creates a strong **type-safety mindset**.

---

