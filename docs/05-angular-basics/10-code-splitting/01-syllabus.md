# Syllabus - **10. Code Splitting**

- [ ] 10.1 Code Splitting via Module
- [ ] 10.2 Code Splitting for standalone component

## Brief Theory

**Code splitting in Angular** is a technique used to **break a large application into smaller JavaScript bundles** so that only the code needed for a specific feature or route is loaded **when it’s needed**, instead of loading everything at once.

This improves **performance**, especially for large apps.

---

## Why code splitting is important

Without code splitting:

- The browser downloads the **entire app upfront**
- Slower initial load time
- Worse experience on slow networks or low-end devices

With code splitting:

- Smaller initial bundle
- Faster first load 🚀
- Features load **on demand**

---

## How Angular does code splitting

Angular mainly supports code splitting through **lazy loading**.

### 1. Lazy loading modules (most common)

Angular splits code automatically when you lazy-load a module.

### Example (Angular Routing)

**Before (eager loading):**

```ts
import { AdminModule } from "./admin/admin.module";

const routes: Routes = [{ path: "admin", component: AdminComponent }];
```

**After (lazy loading):**

```ts
const routes: Routes = [
  {
    path: "admin",
    loadChildren: () =>
      import("./admin/admin.module").then((m) => m.AdminModule),
  },
];
```

➡️ The `AdminModule` is downloaded **only when the user visits `/admin`**.

---

### 2. Standalone components (Angular 14+)

Angular can lazy-load **standalone components** too.

```ts
const routes: Routes = [
  {
    path: "profile",
    loadComponent: () =>
      import("./profile/profile.component").then((c) => c.ProfileComponent),
  },
];
```

This also creates a separate bundle.

---

## What gets split?

Angular’s build system (Webpack or esbuild) splits:

- Lazy-loaded modules
- Lazy-loaded components
- Their dependencies

Each lazy-loaded feature becomes a **separate JavaScript chunk**.

---

## Benefits recap

✅ Faster initial load
✅ Better performance
✅ Reduced memory usage
✅ Scales well for large apps

---

## When should you use code splitting?

- Large Angular apps
- Feature-heavy dashboards
- Admin panels
- Apps with many routes

---

### Simple definition (for exams/interviews)

> **Code splitting in Angular** is the process of dividing an application into smaller bundles that are loaded on demand, mainly using lazy loading, to improve performance and reduce initial load time.
