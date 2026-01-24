# Template Driven Forms

Let's learn template driven forms in angular. \
We will be building a blogpost app.

## Project Metadata

- repository: https://github.com/neutral-00/practice-angular
- parent branch: main
- branch: 16-template-forms

## Scenario

- Let's create a template driven form to publish a post.
- Create a component name `src/app/blogpost/blogpost.component.ts`
- Keep a heading with the wording of `Create Post`
- Below it keep an input text with the placeholder of `Post Title`
- Below it keep a text area with a max character length of 500.
  - Keep placeholder text as `Post body...`
- Below it keep a input text with the placeholder of `Author Name`
- Below it keep a publish button
- Below it, in a different section keep a header with wording of `Recent Post`
- Display list of post ordered based on most recent ones
- Make them collased by default, but should be expandable
- Update the `src/app/app.routes.ts` to load this component in a route.
- Also create a `Post` model with the following fields
  - id: string;
  - title: string;
  - text: string;
  - author: string;
  - publishedOn: number;

## Technology Stake

- Angular 21
- Angular Material
- Tailwindcss
- Json Server

## Steps

### 1. Enable Template Driven Forms

Angular template-driven forms require `FormsModule`.

Update `src/app/app.config.ts`:

```ts
import { ApplicationConfig } from "@angular/core";
import { provideRouter } from "@angular/router";
import { FormsModule } from "@angular/forms";
import { importProvidersFrom } from "@angular/core";
import { routes } from "./app.routes";

export const appConfig: ApplicationConfig = {
  providers: [provideRouter(routes), importProvidersFrom(FormsModule)],
};
```

---

### 2. Create Blog Post Component

Generate the component:

```bash
ng g c blogpost --type=component --style none
```

This creates:

```
src/app/blogpost/
  ├── blogpost.component.ts
  ├── blogpost.component.html
  ├── blogpost.component.spec.ts
```

---

### 3. Define the Post Model

Create a shared model file:

`src/app/models/post.model.ts`

```ts
export interface Post {
  id: string;
  title: string;
  text: string;
  author: string;
  publishedOn: number;
}
```

> `publishedOn` is stored as milliseconds to avoid timezone-related issues and allow easy local conversion in the browser.

---

### 4. Configure JSON Server

_Note_

- json server was already installed in the main branch
- Just for your info we ran the command `pnpm add -D json-server@0.17.4`

Create `db.json` at project root:

```json
{
  "posts": []
}
```

Run JSON Server:

```bash
npx json-server --watch db.json --port 3000
```

---

### 5. Create Blog Post Service

Generate a service:

```bash
ng generate service services/post
```

`src/app/services/post.service.ts`

```ts
import { HttpClient } from "@angular/common/http";
import { Injectable } from "@angular/core";
import { Post } from "../models/post.model";
import { Observable } from "rxjs";

@Injectable({
  providedIn: "root",
})
export class PostService {
  private apiUrl = "http://localhost:3200/posts";

  constructor(private http: HttpClient) {}

  createPost(post: Post): Observable<Post> {
    return this.http.post<Post>(this.apiUrl, post);
  }

  getPosts(): Observable<Post[]> {
    return this.http.get<Post[]>(this.apiUrl);
  }
}
```

Ensure `HttpClient` is enabled in `app.config.ts`:

```ts
import { provideHttpClient } from "@angular/common/http";

providers: [
  provideRouter(routes),
  importProvidersFrom(FormsModule),
  provideHttpClient(),
];
```

---

### 6. BlogPost Component Logic

`src/app/blogpost/blogpost.component.ts`

```ts
import { Component, OnInit } from "@angular/core";
import { Post } from "../models/post.model";
import { PostService } from "../services/post.service";

@Component({
  selector: "app-blogpost",
  templateUrl: "./blogpost.component.html",
})
export class BlogpostComponent implements OnInit {
  posts: Post[] = [];

  model: Partial<Post> = {
    title: "",
    text: "",
    author: "",
  };

  constructor(private postService: PostService) {}

  ngOnInit(): void {
    this.loadPosts();
  }

  publish(): void {
    const newPost: Post = {
      id: crypto.randomUUID(),
      title: this.model.title!,
      text: this.model.text!,
      author: this.model.author!,
      publishedOn: Date.now(),
    };

    this.postService.createPost(newPost).subscribe(() => {
      this.model = { title: "", text: "", author: "" };
      this.loadPosts();
    });
  }

  loadPosts(): void {
    this.postService.getPosts().subscribe((posts) => {
      this.posts = posts.sort((a, b) => b.publishedOn - a.publishedOn);
    });
  }
}
```

---

### 7. Template Driven Form (HTML)

`src/app/blogpost/blogpost.component.html`

```html
<div class="max-w-2xl mx-auto p-6">
  <h1 class="text-2xl font-semibold mb-4">Create Post</h1>

  <form #postForm="ngForm" (ngSubmit)="publish()" class="space-y-4">
    <mat-form-field class="w-full">
      <mat-label>Post Title</mat-label>
      <input
        matInput
        name="title"
        placeholder="Post Title"
        required
        [(ngModel)]="model.title"
      />
    </mat-form-field>

    <mat-form-field class="w-full">
      <textarea
        matInput
        name="text"
        placeholder="Post body..."
        maxlength="500"
        rows="5"
        required
        [(ngModel)]="model.text"
      >
      </textarea>
      <mat-hint align="end">{{ model.text?.length || 0 }}/500</mat-hint>
    </mat-form-field>

    <mat-form-field class="w-full">
      <input
        matInput
        name="author"
        placeholder="Author Name"
        required
        [(ngModel)]="model.author"
      />
    </mat-form-field>

    <button
      mat-raised-button
      color="primary"
      type="submit"
      [disabled]="postForm.invalid"
      class="cursor-pointer"
    >
      Publish
    </button>
  </form>

  <section class="mt-10">
    <h2 class="text-xl font-semibold mb-4">Recent Post</h2>

    <mat-accordion>
      <mat-expansion-panel *ngFor="let post of posts">
        <mat-expansion-panel-header>
          <mat-panel-title> {{ post.title }} </mat-panel-title>
          <mat-panel-description>
            {{ post.author }} • {{ post.publishedOn | date:'medium' }}
          </mat-panel-description>
        </mat-expansion-panel-header>

        <p class="whitespace-pre-line">{{ post.text }}</p>
      </mat-expansion-panel>
    </mat-accordion>
  </section>
</div>
```

---

## Common Standalone Angular Errors

- ❌ No directive found with exportAs 'ngForm'
  → Import `FormsModule` in the component

- ❌ mat-form-field is not a known element
  → Import the required Angular Material modules in the component

- ❌ Can't bind to 'ngModal'
  → Typo: should be `ngModel`

### 8. Update Routing

`src/app/app.routes.ts`

```ts
import { Routes } from "@angular/router";
import { BlogpostComponent } from "./blogpost/blogpost.component";

export const routes: Routes = [
  { path: "", redirectTo: "/post", pathMatch: "full" },
  { path: "post", component: BlogpostComponent },
];
```

---

### 9. What This Tutorial Demonstrates

- Template-driven form basics (`ngModel`, `ngForm`)
- Validation using HTML + Angular
- Angular Material + Tailwind integration
- JSON Server CRUD
- Sorting data by timestamp
- Expandable UI using `mat-expansion-panel`

---

Now is a great place to pause and **crystallize the learning**.

---

## Summary: What We Learned in This Project

This project walked through building a **real-world, form-driven feature** using **Angular 21**, while intentionally embracing its **standalone and zoneless architecture**.

---

### 1. Standalone Components Are the New Default

- Angular 21 applications are **standalone by default**
- Every component acts like its **own NgModule**
- UI features must be imported **at the component level**

**Key takeaway**

> `app.config.ts` is for providers,
> component `imports` are for templates.

---

### 2. Template-Driven Forms Still Matter

Despite newer APIs, **template-driven forms are still valid and supported**.

We learned:

- How to use `ngForm` and `ngModel`
- How validation is driven by HTML attributes
- Why template-driven forms rely on **mutable fields**

**Important nuance**

> Template-driven forms do not integrate directly with signals — and that’s okay.

---

### 3. Common Standalone Pitfalls (and How to Fix Them)

We encountered and fixed real Angular errors:

| Error                                       | Root Cause              | Fix                 |
| ------------------------------------------- | ----------------------- | ------------------- |
| `No directive found with exportAs 'ngForm'` | `FormsModule` missing   | Import in component |
| `mat-form-field is not a known element`     | Material module missing | Import in component |
| `Can't bind to 'ngModal'`                   | Typo                    | Use `ngModel`       |

These are **classic Angular 16+ migration issues**.

---

### 4. Angular Material in Standalone Apps

- Angular Material modules must be imported **per component**
- Using a shared `MATERIAL_IMPORTS` array improves readability
- Material works seamlessly with Tailwind utility classes

---

### 5. Zoneless Angular Does Not Mean “Signals Everywhere”

Angular 21 is **zoneless by default**, but:

- Signals are **recommended**, not mandatory
- Template-driven forms still expect **plain properties**
- Signals shine for:
  - Application state
  - Derived values
  - UI behavior

We used **both**, intentionally.

---

### 6. Signals for Application State

We introduced signals for post state:

```ts
posts = signal<Post[]>([]);
```

Benefits:

- Immediate UI updates
- No manual change detection
- Perfect fit for zoneless Angular

Signals handled **what the app shows**,
forms handled **how the user inputs data**.

---

### 7. Resetting Forms the Right Way

We learned an important Angular form lesson:

- Resetting the model ≠ resetting the form
- Resetting the form state requires `NgForm.resetForm()`

Using:

- `#postForm="ngForm"`
- `@ViewChild('postForm')`

allowed us to restore a **pristine, untouched form** after submission.

---

### 8. Proxy Configuration for Local Development

To avoid CORS issues:

- Created `proxy.conf.json`
- Routed API calls via `/api`
- Kept service URLs environment-agnostic

This is a **production-ready development setup**.

---

### 9. Clean Separation of Concerns

We kept responsibilities clear:

| Layer     | Responsibility         |
| --------- | ---------------------- |
| Component | UI + orchestration     |
| Template  | Validation + structure |
| Service   | HTTP communication     |
| Model     | Type safety            |
| Signals   | Application state      |

This makes the code:

- Testable
- Readable
- Scalable

---

### Final Thought

This project was not just about **forms** —
it was about learning how **modern Angular actually works**:

- Standalone-first
- Zoneless by default
- Signals where they make sense
- Pragmatism over dogma

> Angular 21 doesn’t force a single paradigm —
> it lets you compose the right tools for the job.

---

check out the Validators class: https://angular.io/api/forms/Validators - these are all built-in validators, though that are the methods which actually get executed (and which you later can add when using the reactive approach).

For the template-driven approach, you need the directives. You can find out their names, by searching for "validator" in the official docs: https://angular.io/api?type=directive - everything marked with "D" is a directive and can be added to your template.

Additionally, you might also want to enable HTML5 validation (by default, Angular disables it). You can do so by adding the ngNativeValidate to a control in your template.
