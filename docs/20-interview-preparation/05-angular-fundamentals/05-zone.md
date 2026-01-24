
# Zone.js

## Q. Why was zone.js removed from angular?

Zone.js used to check the entire component tree for changes whenever an event occured. This could be heavy on performance. Signals on the other hand allow angular to know exactly which part of a template needs to be updated.
This lead to much faster rendering.


## Q. How to identify if an angular project is zoneless?

---
To determine if an Angular project was created with the zoneless option enabled (via `ng new --zoneless` flag in Angular 18+), check these key configuration files for zoneless-specific setups.[3][4][5]

## app.config.ts
Look for `provideZonelessChangeDetection()` (stable in Angular 19+) or `provideExperimentalZonelessChangeDetection()` in the providers array:
```typescript
import { provideZonelessChangeDetection } from '@angular/core';

export const appConfig: ApplicationConfig = {
  providers: [
    provideZonelessChangeDetection(),  // Zoneless indicator
    // other providers
  ]
};
```
Absence of zone-related providers confirms zoneless mode.[2][6][3]

## angular.json
Verify the `polyfills` array is empty or excludes `zone.js`:
```json
"build": {
  "options": {
    "polyfills": []  // No zone.js = zoneless
  }
}
```
Zoneless projects remove Zone.js entirely post-generation.[4][5]

## main.ts and package.json
- `main.ts` uses `bootstrapApplication` without Zone.js imports.
- Run `npm ls zone.js`—should show "not found" or manually uninstalled.[1][3]

---
