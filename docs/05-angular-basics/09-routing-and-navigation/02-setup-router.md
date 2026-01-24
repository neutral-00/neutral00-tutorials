# Setup Routing

Routing comes by default, when an angular project is created using the angular cli.

However, if somehow if it was skipped, you can add again with this command `ng add @angular/router`
Then update the files as in the steps below:

Great switch of context 🚀 — let’s walk through how to add **routes** to an existing Angular app. Since you’re already hands‑on with Angular 21, I’ll show you the idiomatic way using the latest standalone APIs, but also note the classic `AppRoutingModule` approach.

---

## ✅ Step 1: Import the Router

- Create a file `src/app/app.routes.ts`
- Angular’s router comes from `@angular/router`.
- add the below import statement

```ts
import { Routes } from "@angular/router";
```

---

## ✅ Step 2: Define Your Routes

Create a `routes` array mapping paths to components.

```ts
import { HomeComponent } from "./home/home.component";
import { AboutComponent } from "./about/about.component";

export const routes: Routes = [
  { path: "", component: HomeComponent }, // default route
  { path: "about", component: AboutComponent }, // /about
  { path: "**", redirectTo: "" }, // wildcard fallback
];
```

---

## ✅ Step 3: Register Router in Your App

### **Standalone app (Angular 15+)**

If your app uses standalone components (no `NgModule`), updated `src/app/app.config.ts`:

```ts
import { bootstrapApplication } from "@angular/platform-browser";
import { provideRouter } from "@angular/router";
import { AppComponent } from "./app/app.component";
import { routes } from "./app/app.routes";

bootstrapApplication(AppComponent, {
  providers: [provideRouter(routes)],
});
```

---

### **Classic NgModule app**

If your app still uses `AppModule`:

```ts
import { NgModule } from "@angular/core";
import { RouterModule, Routes } from "@angular/router";

const routes: Routes = [
  { path: "", component: HomeComponent },
  { path: "about", component: AboutComponent },
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule],
})
export class AppRoutingModule {}
```

Then import `AppRoutingModule` into `AppModule`.

---

## ✅ Step 4: Add Router Outlet

In your root template (`app.component.html`):

```html
<nav>
  <a routerLink="/">Home</a>
  <a routerLink="/about">About</a>
</nav>

<router-outlet></router-outlet>
```

---

## ✅ Step 5: Navigate

- Use `<a routerLink="...">` in templates
- Or programmatically:

```ts
import { Router } from '@angular/router';

constructor(private router: Router) {}

goToAbout() {
  this.router.navigate(['/about']);
}
```

---

### ⚡ Quick Recap

- Define `Routes` array
- Register with `provideRouter()` (standalone) or `RouterModule.forRoot()` (NgModule)
- Add `<router-outlet>` in root template
- Use `routerLink` or `router.navigate()` to move around

---
