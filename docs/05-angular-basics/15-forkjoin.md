Here’s a clean, modern **Angular + RxJS `forkJoin`** example using **Typicode JSONPlaceholder** endpoints. This is the kind of example that actually compiles and runs — no fluff.

I’ll show you:

✅ A service that makes multiple API calls  
✅ A component that uses `forkJoin`  
✅ The expected combined result  
✅ A few pro‑tips so you don’t hit common pitfalls

---

# ✅ **1. Angular Service Using `forkJoin`**

```ts
import { Injectable } from "@angular/core";
import { HttpClient } from "@angular/common/http";
import { forkJoin } from "rxjs";

@Injectable({ providedIn: "root" })
export class ApiService {
  private baseUrl = "https://jsonplaceholder.typicode.com";

  constructor(private http: HttpClient) {}

  loadDashboardData() {
    return forkJoin({
      posts: this.http.get(`${this.baseUrl}/posts`),
      users: this.http.get(`${this.baseUrl}/users`),
      todos: this.http.get(`${this.baseUrl}/todos`),
    });
  }
}
```

### ✅ What this does

- Makes **3 parallel API calls**
- Returns **ONE combined observable**
- Emits **once** when all calls complete
- Emits an object like:

```ts
{
  posts: [...],
  users: [...],
  todos: [...]
}
```

---

# ✅ **2. Component Using the Service**

```ts
import { Component, OnInit } from "@angular/core";
import { ApiService } from "./api.service";

@Component({
  selector: "app-dashboard",
  standalone: true,
  template: `
    <h2 class="text-xl font-bold mb-4">Dashboard</h2>

    <pre>{{ data | json }}</pre>
  `,
})
export class DashboardComponent implements OnInit {
  data: any;

  constructor(private api: ApiService) {}

  ngOnInit() {
    this.api.loadDashboardData().subscribe((result) => {
      this.data = result;
      console.log("ForkJoin result:", result);
    });
  }
}
```

---

# ✅ **3. Expected Output**

The console and template will show something like:

```json
{
  "posts": [ ...100 posts... ],
  "users": [ ...10 users... ],
  "todos": [ ...200 todos... ]
}
```

---

# ✅ **4. Why `forkJoin` is perfect here**

Use `forkJoin` when:

✅ You want **parallel** API calls  
✅ You want the result **only when all calls finish**  
✅ You want **one combined object**  
✅ You don’t need intermediate values

It’s ideal for dashboards, initial page loads, or any “load everything at once” scenario.

---

# ✅ **5. Common Pitfalls (and fixes)**

### ❌ One request errors → whole forkJoin fails

✅ Fix: use `catchError` inside each request if needed.

### ❌ You expect continuous updates

✅ Use `combineLatest` instead of `forkJoin`.

### ❌ You need sequential calls

✅ Use `switchMap` or `concatMap`.

---

If you want, I can also show you:

✅ `forkJoin` with error handling  
✅ `forkJoin` + Angular signals  
✅ `forkJoin` inside a resolver  
✅ `forkJoin` with typed responses (`interface Post`, `User`, etc.)

Just tell me how deep you want to go.
