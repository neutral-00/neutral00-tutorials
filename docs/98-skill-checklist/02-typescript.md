# TypeScript Skill Checklist

Here are list of must have skillsets a senior TypeScript Developer must have.
All these skills will be tested in a git repo: [https://github.com/neutral-00/poc-typescript](https://github.com/neutral-00/poc-typescript)
They will be group by branch name. For example, skills under `Types & Interfaces` will be tested under the git branch `types-interfaces`.

## Types & Interfaces

### Basic Types

1. [] primitive types (string, number, boolean)
2. [] any vs unknown type guards
3. [] never type exhaustive checks
4. [] void vs undefined returns
5. [] literal types ("read" | "write")
6. [] bigint and symbol usage

### Interfaces

7. [] interface Person `{ name: string }`
8. [] readonly properties
9. [] optional ? properties
10. [] index signatures [key: string]
11. [] extends interface inheritance
12. [] Function types parameters

### Advanced Types

13. [] type Person = `{ name: string }`
14. [] union types string | number
15. [] intersection types A & B
16. [] type guards with typeof
17. [] discriminated unions `{ kind: "circle" }`
18. [] mapped types `{ [K in keyof T]: T[K] }`

## Generics

### Core Generics

1. [] function `identity<T>(arg: T): T`
2. [] generic interfaces `Array<T>`
3. [] generic classes `Stack<T>`
4. [] constraints extends `{ length: number }`
5. [] default generics T = string

### Advanced Generics

6. [] conditional types T extends U ? X : Y
7. [] infer keyword infer R
8. [] keyof T type operator
9. [] in operator mapped types
10. [] utility types `Partial<T> Readonly<T>`

## Functions

### Function Types

1. [] () => void signatures
2. [] `Parameters<T> ReturnType<T>`
3. [] `ConstructorParameters<T> InstanceType<T>`
4. [] `ThisParameterType<T> ThisType<T>`
5. [] overload signatures multiple
6. [] rest parameters ...args: any[]

### Advanced Functions

7. [] function overloading signatures
8. [] generic function constraints
9. [] higher-order functions generics
10. [] callback function typing

## Object-Oriented

### Classes

1. [] public private protected modifiers
2. [] readonly properties constructor
3. [] abstract classes methods
4. [] constructor parameter properties
5. [] getters/setters accessors
6. [] static properties methods

### Inheritance

7. [] extends super() calls
8. [] overrides method overriding
9. [] abstract method implementation

## Modules & Namespaces

### ES Modules

1. [] export default vs named
2. [] `import { Type } from "./module"`
3. [] `import \* as Utils from "./utils"`
4. [] export type only types
5. [] re-export `export { A } from "./a"`

### Namespaces

6. [] namespace Utils `{ export class X }`
7. [] triple-slash /// <reference />
8. [] namespace merging augmentation

## Decorators

### Class Decorators

1. [] function sealed(constructor: Function)
2. [] @sealed class BugReport
3. [] constructor parameter access

### Property Decorators

4. [] function format(target: any, key: string)
5. [] property descriptor modification

### Method Decorators

6. [] function enumerable(value: boolean)
7. [] method descriptor writable

### Parameter Decorators

8. [] function required(target: any, key: string, index: number)

### Decorator Factories

9. [] function color(backgroundColor: string)
10. [] @color("red") class BugReport

## Advanced Patterns

### Utility Types

1. [] `Pick<T, K>` selection
2. [] `Omit<T, K>` exclusion
3. [] `Record<K, T>` dictionary
4. [] `Exclude<U, E>` union exclusion
5. [] `Extract<T, U>` union extract

### Template Literal Types

6. [] type EventNames = `on${string}`
7. [] type Keys = "id" | "name"

### Variadic Tuple Types

8. [] type `Concat<T, U> = [...T, ...U]`
9. [] type `Last<T extends any[]> = T[-1]`

## Declaration Files

### .d.ts Files

1. [] declare module "lodash"
2. [] declare namespace NodeJS
3. [] declare global window extensions
4. [] declare class external classes
5. [] ambient module declarations

## Tooling & Configuration

### tsconfig.json

1. [] strict mode settings
2. [] target ES2022 lib dom
3. [] moduleResolution node16
4. [] paths module aliases
5. [] include exclude patterns
6. [] composite incremental builds

### Build Tools

7. [] tsc compiler options
8. [] ts-node runtime execution
9. [] esbuild bundling TypeScript
10. [] swc fast transpilation

## Testing Types

### Jest + TypeScript

1. [] `expect.objectContaining({ id: expect.any(Number) })`
2. [] jest.MockedFunction typing
3. [] jest.spyOn mock implementation
4. [] typed mock return values

### Vitest

5. [] vi.mock() typed mocks
6. [] vi.fn() typed mock functions

## RxJS Typing

### Observables

1. [] `Observable<T> typing`
2. [] `Subject<T> BehaviorSubject<T>`
3. [] `OperatorFunction<A, B> typing`
4. [] pipe(map, filter) generics
5. [] typed operators `switchMap<T, R>`

## Node.js Typing

### Node Types

1. [] import fs from "fs/promises"
2. [] `import { spawn } from "child_process"`
3. [] process.env typing
4. [] Buffer Uint8Array typing
5. [] http ServerRequest handlers

## Performance & Patterns

### Branding Types

1. [] type `Brand<K, T> = K & { \_\_brand: T }`
2. [] type `UserId = Brand<string, "UserId">`

### Opaque Types

3. [] type `Opaque<T, K> = T & { **opaque**: K }`

### Builder Pattern

4. [] class `QueryBuilder<T> fluent`
5. [] chained generic methods

### Factory Functions

6. [] function createUser(): User & Validated
