# Pure Vs Impure Pipes

Pure pipes in Angular execute only when their input reference changes, while impure pipes run on every change detection cycle regardless of input changes. [angularminds](https://www.angularminds.com/blog/pure-vs-impure-pipes-in-angular)

## Key Differences

Pure pipes, the default type, optimize performance by checking primitive values or object references before re-executing the `transform` method. Impure pipes trigger every time Angular's change detection runs, making them suitable for mutable data like arrays but potentially slower. Use pure pipes for static transformations and impure ones sparingly for dynamic scenarios like filtering live data. [youtube](https://www.youtube.com/watch?v=Wbf0Zo6_jz8)

| Aspect              | Pure Pipe                  | Impure Pipe                  |
|---------------------|----------------------------|------------------------------|
| Execution Trigger   | Input reference changes   | Every change detection cycle [angularminds](https://www.angularminds.com/blog/pure-vs-impure-pipes-in-angular) |
| Performance         | High (cached results)     | Lower (frequent calls) [yon](https://yon.fun/pure-vs-impure-pipes/) |
| Declaration         | Default (`pure: true`)    | Explicit (`pure: false`) [angularminds](https://www.angularminds.com/blog/pure-vs-impure-pipes-in-angular) |
| Best For            | Immutable/static data     | Mutable arrays/async data [youtube](https://www.youtube.com/watch?v=Wbf0Zo6_jz8) |

## Pure Pipe Example

Create a pure pipe that doubles a number, re-running only if the input changes:

```typescript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({ name: 'double', pure: true })  // Default is pure
export class DoublePipe implements PipeTransform {
  transform(value: number): number {
    return value * 2;
  }
}
```

Template usage: `{{ count | double }}` updates only on new `count` reference. [angularminds](https://www.angularminds.com/blog/pure-vs-impure-pipes-in-angular)

## Impure Pipe Example

An impure filter pipe for arrays, detecting internal mutations like `push()`:

```typescript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({ name: 'impureFilter', pure: false })
export class ImpureFilterPipe implements PipeTransform {
  transform(items: any[], search: string): any[] {
    if (!items || !search) return items;
    return items.filter(item => 
      item.name.toLowerCase().includes(search.toLowerCase())
    );
  }
}
```

Template: `<li *ngFor="let item of users | impureFilter:query">{{item.name}}</li>` reacts to array mutations instantly. [angularminds](https://www.angularminds.com/blog/pure-vs-impure-pipes-in-angular)
