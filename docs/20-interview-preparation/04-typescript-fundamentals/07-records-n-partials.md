# Records

Records are used to construct object types whose property keys are Keys and whose property values are Type \
as defined in `Record<Keys, Type>`

Example:

```ts

type StudentName = "Pritam" | "Shalini" | "Robin" | "Shiva" | "Anmol";

let janAttendance: Record<StudentName, number>;

janAttendance = {
  Pritam: 10,
  Shalini: 9,
  Robin: 7,
  Shiva: 10,
  Anmol: 8,
};

export { janAttendance };

/*
USAGE:
```ts
import { janAttendance } from "./record-demo";
console.log("Anmol's jan attendance: " + janAttendance.Anmol);
```
*/
```

> `Record` **forces all keys in the union to be present**.


## Question

> What if I want to create an object whose keys can be among `StudentName`
> but should **not be forced to have all of them**?

Example:

```ts
febAttendance = { Robin: 0, Shiva: 0 };
```

---

## ✅ Best & Idiomatic Solution: `Partial<Record<...>>`

### Explanation

* `Record<StudentName, number>` → **all keys required**
* `Partial<T>` → makes **all properties optional**
* Combine them → **subset of allowed keys**

---

### ✅ Solution Code

```ts
type StudentName = "Pritam" | "Shalini" | "Robin" | "Shiva" | "Anmol";

let febAttendance: Partial<Record<StudentName, number>>;

febAttendance = {
  Robin: 0,
  Shiva: 0,
};
```

✔️ Valid
✔️ Type-safe
✔️ Only allows keys from `StudentName`
✔️ Does NOT require all keys

---

## ❌ What Is Still Not Allowed (Correctly)

```ts
febAttendance = {
  Robin: 0,
  John: 5,   // ❌ Error: "John" is not part of StudentName
};
```

This is exactly what we want 👍

---

## Alternative (More Explicit, Less Common)

You *could* write this manually using a mapped type:

```ts
type OptionalAttendance = {
  [K in StudentName]?: number;
};
```

Usage:

```ts
let febAttendance: OptionalAttendance = {
  Robin: 0,
  Shiva: 0,
};
```

But 👆 this is essentially what `Partial<Record<...>>` already does, so the utility-type version is preferred in tutorials.

---

## Credit
> official site `https://www.typescriptlang.org/docs/handbook/utility-types.html#recordkeys-type`
