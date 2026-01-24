# Type System

## Explain Typescripts type system and it's benefits

## TypeScript's Type System and Its Benefits

### 🔍 What Is TypeScript's Type System?

- TypeScript’s type system is a **static, structural type system** that adds optional type annotations to JavaScript. 
- It enables developers to define types for variables, function parameters, return values, and object structures, 
- catching errors at compile time rather than runtime.


### 🧩 Core Features

- **Primitive Types**: `string`, `number`, `boolean`, `null`, `undefined`, `symbol`, `bigint`.
- **Complex Types**: Objects, arrays (`number[]`), tuples (`[string, number]`), enums, and more.
- **Union and Intersection Types**: Combine types (e.g., `string | number`, `A & B`).
- **Generics**: Reusable type parameters (e.g., `Array<T>`, `Promise<T>`).
- **Type Inference**: Automatically deduces types when not explicitly declared.
- **Advanced Types**: Mapped, conditional, and template literal types for sophisticated type manipulation.
- **Any and Unknown**: `any` bypasses type checking; `unknown` is a safer alternative requiring type checks before use.


### Reference
> [geek4geeks](https://www.geeksforgeeks.org/typescript/data-types-in-typescript/)