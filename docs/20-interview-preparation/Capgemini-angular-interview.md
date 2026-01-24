# Capgemini Angular Developer Interview Questions and Answers

## Credit

https://www.ambitionbox.com/interviews/capgemini-interview-questions/angular-developer

---

## Q. What is Multicasting in Angular?

Multicasting in Angular means sharing a single observable execution with multiple subscribers, so they all receive the same data stream without triggering duplicate executions.

---

### 🔎 Detailed Explanation

- **Observables in Angular (RxJS)**  
  Normally, Angular’s observables are _unicast_. This means each subscriber creates its own independent execution of the observable. For example, if two components subscribe to the same HTTP request observable, the request will be executed twice.

- **Multicasting Concept**  
  _Multicasting_ allows **multiple subscribers to share one execution** of an observable. Instead of duplicating work, the observable runs once, and its results are broadcast to all subscribers. This is especially useful for:
  - Avoiding repeated HTTP calls
  - Sharing real-time data streams across components
  - Improving performance and efficiency

- **How It Works**  
  Multicasting is achieved using **RxJS Subjects** or operators like:
  - **`Subject`** → A special type of observable that can multicast values to many observers.
  - **`share()`** → Converts a unicast observable into a multicast one.
  - **`shareReplay()`** → Similar to `share()`, but also replays the last emitted values to new subscribers.

- **Example Scenario**  
  Suppose you fetch user profile data via an HTTP request:
  ```typescript
  const user$ = this.http.get("/api/user").pipe(shareReplay(1));
  ```

  - Without multicasting: Each component subscribing to `user$` would trigger a new HTTP request.
  - With multicasting (`shareReplay(1)`): The HTTP request runs once, and all subscribers get the same result.

---

### ⚡ Key Benefits

- **Efficiency**: Prevents redundant observable executions (e.g., multiple HTTP calls).
- **Consistency**: Ensures all subscribers receive the same data stream.
- **Flexibility**: Useful for real-time updates across multiple components.

---

In short, **multicasting in Angular is about broadcasting one observable execution to many subscribers**, typically using **Subjects or operators like `share()` and `shareReplay()`**. It’s a cornerstone of efficient reactive programming in Angular applications.

Sources:

---

Would you like me to show you a **step-by-step code example** of multicasting with `Subject` and multiple Angular components? That way, you can see how two components can share the same data stream without duplicating work.

---

## Q. What is the difference between child routes and forRoot in Angular?

**Child routes in Angular define nested routing within a feature module, while `forRoot()` is used once in the root module to configure the global router service and application-wide routes.**

---

### 🌐 Detailed Explanation

#### 1. **`RouterModule.forRoot()`**

- **Purpose**:
  - Sets up the **application-wide router service**.
  - Should be called **only once** in the root module (`AppModule`).
- **What it does**:
  - Registers the router service.
  - Configures the main routes of the application.
  - Provides singleton services like `Router`, `ActivatedRoute`, and guards globally.
- **Example**:
  ```typescript
  @NgModule({
    imports: [
      RouterModule.forRoot([
        { path: "", component: HomeComponent },
        { path: "about", component: AboutComponent },
      ]),
    ],
    exports: [RouterModule],
  })
  export class AppRoutingModule {}
  ```

#### 2. **Child Routes (`RouterModule.forChild()`)**

- **Purpose**:
  - Used inside **feature modules** to define **nested or module-specific routes**.
  - Does **not** re-provide the router service (avoids duplication).
- **What it does**:
  - Adds routes that are children of existing routes.
  - Useful for lazy-loaded modules or modular applications.
- **Example**:
  ```typescript
  @NgModule({
    imports: [
      RouterModule.forChild([
        {
          path: "products",
          component: ProductsComponent,
          children: [
            { path: "details/:id", component: ProductDetailsComponent },
          ],
        },
      ]),
    ],
    exports: [RouterModule],
  })
  export class ProductsRoutingModule {}
  ```

---

### 🔑 Key Differences

| Aspect               | `forRoot()`                            | `forChild()`                                  |
| -------------------- | -------------------------------------- | --------------------------------------------- |
| **Usage**            | Root module (`AppModule`)              | Feature modules (lazy-loaded or nested)       |
| **Router Service**   | Provides router service globally       | Does not provide router service again         |
| **Scope**            | Application-wide routes                | Module-specific or nested routes              |
| **Frequency**        | Used **once** in the app               | Can be used in multiple feature modules       |
| **Example Use Case** | Main navigation (Home, About, Contact) | Nested routes (Product details, User profile) |

---

### ✅ Summary

- Use **`forRoot()`** in the root module to configure the **global router** and services.
- Use **`forChild()`** in feature modules to define **child or nested routes** without duplicating the router service.

This separation ensures Angular applications remain modular, scalable, and efficient.

---
