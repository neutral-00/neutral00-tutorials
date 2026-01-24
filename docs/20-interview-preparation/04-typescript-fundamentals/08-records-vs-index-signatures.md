# Record vs Index Signatures

Both `Record` and index signatures are used to describe object shapes in TypeScript,
but they solve **very different problems**.

---

## `Record<K, T>`

Use `Record` when:

- You know all possible keys in advance
- Keys come from a finite union
- You want strong type safety and autocomplete

```ts
type StudentName = "Pritam" | "Shalini" | "Robin";

type Attendance = Record<StudentName, number>;

const janAttendance: Attendance = {
  Pritam: 10,
  Shalini: 9,
  Robin: 8,
};
```

`Record` enforces:

- All keys must be present
- No extra keys are allowed

---

## Index Signatures

Use index signatures when:

- Keys are dynamic or unknown
- You are modeling a dictionary or map
- Data comes from external sources

```ts
type AttendanceMap = {
  [key: string]: number;
};

const febAttendance: AttendanceMap = {
  Robin: 0,
  Shiva: 0,
};
```

Index signatures:

- Allow any key
- Do not provide exhaustiveness or autocomplete
- Are more flexible but less safe

---

## Key Difference

| Aspect       | Record        | Index Signature |
| ------------ | ------------- | --------------- |
| Known keys   | Yes           | No              |
| Finite       | Yes           | No              |
| Autocomplete | Yes           | No              |
| Best for     | Domain models | Dictionaries    |

---
