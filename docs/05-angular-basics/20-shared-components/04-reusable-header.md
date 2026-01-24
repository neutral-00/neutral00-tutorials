# Reusable Header

let's create a reusable sticky header that can be used across projects

🔥 **WARNING**
- I had issues in using images because it required extra build configuration
- So as much as possible, keep the component simple and self sufficient.
- Avoid reference to other references, import directly so that it is part of compliation process

**Note:**
- For presentational components keep them in libs/lousing-ui/src/ui/
- For utility components keep them in libs/lousing-ui/src/util/
- For feature components keep them in libs/lousing-ui/src/feature/

## 1. Logo SVG embedded

```ts
import { CommonModule } from '@angular/common';
import { Component } from '@angular/core';
import { RouterLink } from '@angular/router';

@Component({
  selector: 'lc-header',
  imports: [CommonModule, RouterLink],
  template: `
    <header class="sticky top-0 z-10 flex px-6 py-1 bg-gray-100">
      <!-- Left section : lousing logo -->
      <a routerLink="/">
        <!-- compnay logo svg goes here -->
       Logo 
      </a>
      <!-- Right group -->
      <div class="ml-auto flex items-center gap-4">
        <ng-content></ng-content>
      </div>
    </header>
  `,
  styles: ``,
})
export class Header {}
```

