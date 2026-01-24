# View Encaptulation In Angular


- **What are the three types of View Encapsulation in Angular?**
  - `Emulated` (default, styles scoped to the current component via attribute selectors)
  - `None` (global styles, no encapsulation)
  - `ShadowDom` (native browser shadow DOM isolation).
- **Which encapsulation mode is the default in Angular, and why?**  
  `Emulated` is default because it balances isolation with broad browser support.

---

### Practical Usage Questions

- **How does Angular implement `Emulated` encapsulation under the hood?**  
  Expect to describe how Angular rewrites CSS selectors with unique attributes to scope styles.
- **When would you use `ViewEncapsulation.None`?**  
  For global theming or when you want styles to cascade across multiple components.
- **What are the trade‑offs of using `ShadowDom` encapsulation?**  
  Strong isolation and native scoping, but limited browser support in older environments and harder global theming.

---

### Advanced/Scenario Questions

- **How do global styles interact with encapsulated component styles?**  
  Interviewers want you to explain precedence and how global styles can still override component styles if selectors are stronger.
- **Can you combine Angular’s View Encapsulation with CSS variables or TailwindCSS?**  
  This tests your ability to integrate modern styling approaches with Angular’s encapsulation system.
- **How would you debug style leakage between components?**  
  Expect to mention checking encapsulation mode, inspecting DOM attributes, and using Angular DevTools.

---


### Quick Comparison Table

| Mode          | How It Works                           | Pros                               | Cons                                         |
| ------------- | -------------------------------------- | ---------------------------------- | -------------------------------------------- |
| **Emulated**  | Adds unique attributes to scope styles | Default, good balance, widely used | Can still be overridden by global CSS        |
| **None**      | No scoping, styles are global          | Useful for themes, shared styles   | Risk of style leakage, conflicts             |
| **ShadowDom** | Native browser shadow DOM isolation    | True isolation, modern approach    | Limited global theming, older browser issues |

---
