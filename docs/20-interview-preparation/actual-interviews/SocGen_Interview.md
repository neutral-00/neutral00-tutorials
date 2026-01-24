Company: Society General
Position: Java + Angular Lead
Date: 2025-10-03
Time: 12:00 - 12:45 PM IST

## Typescript Questions

Q. Differences among any, unknown and never. When will you use them?
A.

- **any** allows any type and disables type checking. Use when the type is dynamic or unknown at design time.
- **unknown** represents any value but requires type checking before operations. Safer alternative to any.
- **never** represents values that never occur, like functions that always throw or infinite loops. Used for exhaustive checks.

Here are code examples illustrating the use cases of TypeScript's special types: any, unknown, and never.

```typescript
// any allows any value with no type checking
let dataAny: any;
dataAny = 42; // OK
dataAny = "hello"; // OK
dataAny.method(); // OK at compile time, might fail at runtime

// unknown is safer; you must narrow the type before use
let dataUnknown: unknown;
dataUnknown = 42;
dataUnknown = "hello";
// dataUnknown.method();  // Error: Object is of type unknown

// Narrowing unknown with type check
if (typeof dataUnknown === "string") {
  console.log(dataUnknown.toUpperCase()); // OK inside this block
}

// never represents values that never occur, e.g., a function that always throws
function errorThrower(message: string): never {
  throw new Error(message);
}

// Usage of never for exhaustive checks in a switch
type Shape =
  | { kind: "circle"; radius: number }
  | { kind: "square"; side: number };

function area(shape: Shape): number {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2;
    case "square":
      return shape.side * shape.side;
    default:
      const _exhaustiveCheck: never = shape; // Error if not all cases handled
      return _exhaustiveCheck;
  }
}
```

Summary:

- Use `any` when you want to disable type checking but be cautious as it skips safety.
- Use `unknown` for safer handling of dynamic types by forcing explicit checks.
- Use `never` for functions that do not return (throw or loop forever) and for compile-time exhaustive checks in union types to ensure all cases are handled.

---

Q. Explain me the concepts of Type vs Interface in typescript.
A.

- **Interface** defines a contract for object shapes, supports declaration merging, can be implemented by classes, and is better for object-oriented designs.
- **Type** aliases are more versatile, supporting primitives, unions, intersections, tuples, and conditional types. They can't merge declarations.
- Prefer interfaces for object shapes and types for other use cases.

---

Q. Tell me what you know about Generics and Partials.
A.

- Generics provide a way to create reusable components that work with any data type while preserving type safety.
- `Partial<T>` is a utility type that makes all properties of T optional, useful for updating subsets of objects.

Q. What are records in Typescript?
A.

- `Record<K, T>` is a utility type to create an object type with keys of type K and values of type T, useful for mapping property names to types.

Q. Explain Enums and show one usage of it.
A.

- Enums define a set of named constants, which can be numeric or string based.
- Example usage: `enum Direction { Up, Down, Left, Right }` can be used to represent direction states in code.

## Angular Questions

Q. You are using standalone components, how will you bring other dependencies. Explain with code example.
A.

- In an Angular standalone component, dependencies can be imported directly in the `imports` array of the component decorator.

```ts
@Component({
  standalone: true,
  selector: "app-example",
  templateUrl: "./example.component.html",
  imports: [CommonModule, FormsModule],
})
export class ExampleComponent {}
```

Q. Explore more on new angular 18 features like Signal.
A.

- Angular 18 introduces reactive primitives called Signals, which allow fine-grained reactive state management with better performance and simpler reactivity models.

Q. Explain how will you implement inter-component communications that prevents tight coupling.
A.

- Use Angular services with RxJS Subjects or Observables to share data between components without direct references, promoting loose coupling.

Q. Help me understand the importance of tsconfig? what you can configure here?
A.

- tsconfig.json configures the TypeScript compiler settings, including target ECMAScript version, module resolution, strictness options, paths, and more, to control how code is compiled.

Q. Is there an in-built feature in angular to pass credentials in api calls?
A.

- Angular HttpClient allows you to send credentials with requests using options like `{ withCredentials: true }` to include cookies or authorization headers.

## Java Questions

Q. Why we have int as well as Integer in Java?
A.

- `int` is a primitive data type with better performance.
- `Integer` is an object wrapper class that allows null values and provides utility methods, needed for collections and generics.

Q. What are streams in Java? Give me some tail methods.
A.

- Streams represent sequences of elements supporting aggregate operations like map, filter, and reduce.
- Tail methods include `skip()`, `limit()`, `distinct()`, `sorted()` which control the stream processing flow.

Q. How do you bundle your frontend and backend codes? And how do you deploy?
A.

- Frontend code is typically bundled using tools like Webpack or Angular CLI into static assets.
- Backend code (Spring Boot) is packaged as a JAR or WAR.
- Both are deployed on servers or cloud platforms, with frontend often served by CDN or web servers, backend as microservices or APIs.
