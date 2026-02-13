# 🛣️ Setup Routing: Modern vs. Classic

Angular routing is typically initialized via the CLI. If you need to add it manually, use `ng add @angular/router`. Here is how to configure it using both the **Modern (Standalone)** and **Classic (NgModule)** approaches.

---

## ✅ Step 1: Define Your Routes

Regardless of your app's architecture, your route definitions look the same. Create a file `src/app/app.routes.ts`.

```ts
import { Routes } from "@angular/router";
import { HomeComponent } from "./home/home.component";
import { AboutComponent } from "./about/about.component";

export const routes: Routes = [
  { path: "", component: HomeComponent },         // Default route
  { path: "about", component: AboutComponent },   // /about
  { path: "**", redirectTo: "" },                 // Wildcard fallback
];

```

---

## ✅ Step 2: Register the Router

This is where the syntax diverges significantly between modern and older versions of Angular.

### **The Modern Way (Angular 15+ Standalone)**

Modern Angular apps avoid `AppModule`. Instead, you register the router in `app.config.ts` using **Functional Providers**.

```ts
// src/app/app.config.ts
import { ApplicationConfig } from '@angular/core';
import { provideRouter, withComponentInputBinding } from '@angular/router';
import { routes } from './app.routes';

export const appConfig: ApplicationConfig = {
  providers: [
    provideRouter(
      routes, 
      withComponentInputBinding() // Modern extra: maps route params to @Input()
    )
  ]
};

```

### **The Classic Way (NgModule)**

In older projects (or if you prefer Modules), you use the `RouterModule` and a separate `AppRoutingModule`.

```ts
// src/app/app-routing.module.ts
import { NgModule } from "@angular/core";
import { RouterModule, Routes } from "@angular/router";
import { routes } from "./app.routes";

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule],
})
export class AppRoutingModule {}

```

*Don't forget to add `AppRoutingModule` to the `imports` array in your `app.module.ts`.*

---

## ✅ Step 3: Add the Router Outlet

In your root template (`app.component.html`), you must provide a "placeholder" where components will be swapped in and out.

```html
<nav>
  <a routerLink="/" routerLinkActive="active-class">Home</a>
  <a routerLink="/about" routerLinkActive="active-class">About</a>
</nav>

<router-outlet></router-outlet>

```

---

## ✅ Step 4: Programmatic Navigation

If you need to move users based on an action (like a button click or a successful login), use the `Router` service.

### **Modern "Signal-Ready" Syntax**

In modern Angular, we often use the `inject` function instead of the constructor.

```ts
import { Component, inject } from '@angular/core';
import { Router } from '@angular/router';

@Component({ ... })
export class MyComponent {
  private router = inject(Router); // Modern injection

  goToAbout() {
    this.router.navigate(['/about']);
  }
}

```

### **Classic Constructor Syntax**

```ts
constructor(private router: Router) {}

goToAbout() {
  this.router.navigate(['/about']);
}

```

---

## ⚡ Comparison Summary

| Feature | Modern (Standalone) | Classic (NgModule) |
| --- | --- | --- |
| **Registration** | `provideRouter(routes)` | `RouterModule.forRoot(routes)` |
| **Location** | `app.config.ts` | `app-routing.module.ts` |
| **Configuration** | `withX()` functions (e.g., `withViewTransitions()`) | Configuration Object `{ useHash: true }` |
| **Injection** | `inject(Router)` | `constructor(private router: Router)` |

---

Would you like to see how the **Modern Approach** handles **Lazy Loading**? It's much cleaner than the old `loadChildren` string-based syntax!
