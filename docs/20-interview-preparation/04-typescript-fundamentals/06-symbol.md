# Symbol type in Typescript

A common use case for the `symbol` type in TypeScript is to **create unique, non-enumerable property keys** that avoid naming conflicts and simulate private members.

For example, you can use symbols to add metadata to an object without risking property name collisions:

```ts
const metadata = Symbol("metadata");

const user = {
  name: "Alice",
  [metadata]: { role: "admin" }
};

// Access metadata safely
console.log(user[metadata]); // { role: "admin" }

// Symbol properties don't appear in Object.keys()
console.log(Object.keys(user)); // ["name"]
```

This ensures encapsulation and prevents accidental exposure during iteration or JSON serialization.

