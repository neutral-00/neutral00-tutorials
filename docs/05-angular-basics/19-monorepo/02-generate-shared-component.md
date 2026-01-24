# Generate Shared component

Let's generate a share component in the library project lousing-ui.
```sh
cd lousing-ui/src
ng g c components/header --inline-template --inline-style --skip-tests --flat --dry-run
```

Update the content with:
```ts
import { CommonModule } from '@angular/common';
import { Component } from '@angular/core';

@Component({
  selector: 'lc-header',
  imports: [CommonModule],
  template: `
    <header class="sticky top-0 z-10 flex px-6 py-4 bg-cyan-300">
      <!-- Left section : logo -->
      <a href="http://github.com/neutral00" target="_blank" rel="noopener noreferrer">
        <img src="./assets/icons/lousing-logo.svg" alt="lousing logo" class="h-8 w-auto" />
      </a>
      <!-- Right group -->
      <div class="ml-auto flex items-center gap-4">
        <ng-content select="[right]"></ng-content>
      </div>
    </header>
  `,
  styles: ``,
})
export class Header {}
```

Create `src/components/index.ts` with the below content
```ts
export * from './header';
```

Next update `src/public-api.ts` as 
```ts
/*
 * Public API Surface of lousing-ui
 */
export * from './components';
export * from './lib/lousing-ui';
```

Build the project by navigating to the root of the project and run
```sh
ng build lousing-ui --watch
```
Now you can use it in another app by importing it
```ts
import {Header} from 'lousing-ui';
```

In another terminal run `ng serve `

**Note**
- Generating a library with the Angular CLI automatically adds its path to the tsconfig file. The Angular CLI uses the tsconfig paths to tell the build system where to find the library.
- You just have to rebuild your library whenever you make changes to it
- The above command with --watch does incremental build, improving library DX
