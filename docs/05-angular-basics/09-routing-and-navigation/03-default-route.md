# Setup Default Route

Update your route like the one below, don't forget to make sure it is in the first entry.

```ts
import { Routes } from "@angular/router";
import { TaskShellComponent } from "./components/task-shell/task-shell.component";

export const routes: Routes = [
  { path: "home", component: TaskShellComponent },
  { path: "", redirectTo: "/home", pathMatch: "full" },
];
```
