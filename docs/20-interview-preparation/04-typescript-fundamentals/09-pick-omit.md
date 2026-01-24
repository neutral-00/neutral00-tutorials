# Pick and Omit in TypeScript

`Pick` and `Omit` are **utility types** used to create new object types by
**selecting** or **excluding** properties from an existing type.

They help you:

- Avoid type duplication
- Model API contracts
- Create safer, intention-revealing types

---

## Base Type (Starting Point)

```ts
type Student = {
  id: number;
  name: string;
  email: string;
  age: number;
  attendance: number;
};
```

This represents the **full domain model**.

---

## `Pick<T, K>`

### What It Does

> Creates a new type by **picking only the specified keys** from `T`.

Syntax:

```ts
Pick<Type, Keys>;
```

---

### Example: Public Student Info

```ts
type StudentPublicInfo = Pick<Student, "id" | "name">;

const student: StudentPublicInfo = {
  id: 1,
  name: "Robin",
};
```

✔️ Only selected fields are allowed
❌ Missing fields are removed
❌ Extra fields are not permitted

---

### Common Use Cases for Pick

- API response DTOs
- UI view models
- Limiting exposed data

```ts
type StudentListItem = Pick<Student, "id" | "name" | "attendance">;
```

---

## `Omit<T, K>`

### What It Does

> Creates a new type by **removing specified keys** from `T`.

Syntax:

```ts
Omit<Type, Keys>;
```

---

### Example: Student Without Sensitive Info

```ts
type StudentWithoutEmail = Omit<Student, "email">;

const student: StudentWithoutEmail = {
  id: 1,
  name: "Robin",
  age: 20,
  attendance: 95,
};
```

✔️ All fields except `email` remain
❌ `email` cannot be used

---

### Common Use Cases for Omit

- Removing sensitive fields
- Creating write/update payloads
- Excluding server-generated values

```ts
type CreateStudentPayload = Omit<Student, "id">;
```

---

## Pick vs Omit (When to Use Which)

| Scenario                                           | Prefer |
| -------------------------------------------------- | ------ |
| You want **only a few fields**                     | `Pick` |
| You want **almost everything except a few fields** | `Omit` |
| API responses                                      | `Pick` |
| Form payloads                                      | `Omit` |

📌 **Rule of thumb**

- _Small subset?_ → `Pick`
- _Small exclusion?_ → `Omit`

---

## Pick / Omit Are Type-Safe

```ts
type InvalidPick = Pick<Student, "name" | "phone">;
// ❌ Error: "phone" does not exist on type Student
```

This is what makes them superior to manually writing new interfaces.

---

## Combining with Other Utility Types

### Pick + Partial

```ts
type StudentUpdatePayload = Partial<
  Pick<Student, "email" | "age" | "attendance">
>;
```

Allows updating **any subset** of selected fields.

---

### Omit + Readonly

```ts
type ReadonlyStudent = Readonly<Omit<Student, "attendance">>;
```

---

## How Pick and Omit Work (Mental Model)

- `Pick` = **whitelist**
- `Omit` = **blacklist**

Both:

- Preserve property types
- Stay in sync if the base type changes
- Reduce duplication

---

## Summary

- `Pick` selects specific properties
- `Omit` removes specific properties
- Both improve safety and maintainability
- Prefer them over redefining object types

---

## Credit

> Official docs
> [https://www.typescriptlang.org/docs/handbook/utility-types.html#picktype-keys](https://www.typescriptlang.org/docs/handbook/utility-types.html#picktype-keys)
> [https://www.typescriptlang.org/docs/handbook/utility-types.html#omittype-keys](https://www.typescriptlang.org/docs/handbook/utility-types.html#omittype-keys)

---

### Teaching Tip (Optional Note)

Encourage learners to:

- Define **one source-of-truth type**
- Derive all other types using utility types

This leads to **refactor-friendly TypeScript**.

---
