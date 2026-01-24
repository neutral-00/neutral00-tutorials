# 20 – Todo App (Vanilla JavaScript)

## Introduction

In this tutorial, we will build a **Kanban-style Todo application** using **vanilla JavaScript**.

The goal is to understand how a small but complete application can be built **without frameworks**, while still following clean structure, separation of concerns, and modern tooling practices.

We will use:

- **Vite** for development setup
- **Vanilla JavaScript** for UI and state handling
- **Tailwind CSS** for layout and styling
- **Axios** for API communication
- **JSON Server** as a lightweight backend

---

## Project Metadata

- **Repository:** [https://github.com/neutral-00/practice-js](https://github.com/neutral-00/practice-js)
- **Parent branch:** `main`
- **Working branch:** `20-todo-app`

---

## Learning Objectives

By the end of this tutorial, you will learn how to:

- Structure a vanilla JavaScript application
- Build a Kanban-style layout using Tailwind Grid/Flexbox
- Manage application state without frameworks
- Perform CRUD operations using Axios
- Move items between logical states (to-do → in-progress → done)
- Integrate a frontend app with a mock REST API

---

## Application Requirements

### Todo Status Columns

The application will display todos in **three columns**:

1. **To-Do**
2. **In-Progress**
3. **Done**

Each todo belongs to exactly one status.

---

### Todo Actions

Each todo card will display buttons based on its current status:

| Status      | Available Actions     |
| ----------- | --------------------- |
| To-Do       | Move Right            |
| In-Progress | Move Left, Move Right |
| Done        | Move Left             |

Actions will update the todo’s status and persist the change via an API call.

---

### Add Todo Form

The application will include a form to:

- Enter a todo title
- Add a new todo with default status `todo`
- Persist the new todo using the backend API

---

## Backend Choice: JSON Server

For this tutorial, we will use **JSON Server** as a mock backend.

### Why JSON Server?

- No backend code required
- Instant REST API
- Perfect for frontend-focused learning
- Supports all CRUD operations needed for this app

This allows us to focus on **JavaScript logic and UI**, not backend setup.

---

## Setting Up JSON Server

### Install JSON Server

From the project root:

```bash
pnpm add -D json-server@0.17.4
```

---

### Create Database File

Create a file named `db.json` in the project root:

```json
{
  "todos": [
    {
      "id": 1,
      "title": "Learn Vanilla JavaScript",
      "status": "todo"
    }
  ]
}
```

---

Create `routes.json` with the below content

```json
{
  "/api/*": "/$1"
}
```

### Start the Server

Run:

```bash
pnpm dlx json-server --watch db.json --port 3300 --routes routes.json
```

or add below to `package.json > scripts`

```
{
  "scripts": {
    "server": "json-server --watch db.json --port 3300 --routes routes.json"
  }
}
```

Then you can run `pnpm run server`
Once started, the following endpoints will be available:

- `GET /api/todos`
- `POST /api/todos`
- `PATCH /api/todos/:id`
- `DELETE /api/todos/:id`

The API base URL will be:

```text
http://localhost:3300/api
```

---

## Data Model

Each todo item follows this structure:

```ts
Todo {
  id: number;
  title: string;
  status: "todo" | "in-progress" | "done";
}
```

This simple model maps directly to:

- UI columns
- Movement logic
- API requests

---

### ✔️ End of Section

At this point:

- The project branch is ready
- The backend is running
- The data model is clearly defined

---

## Section 4 – Application Layout with Tailwind CSS

In this section, we will build the **visual layout** of the Todo application using **Tailwind CSS**.

The layout follows a **Kanban-style board**, where todos are grouped by their status and displayed in separate columns.

---

## Layout Requirements

- Three columns:
  - **To-Do**
  - **In-Progress**
  - **Done**

- Responsive layout:
  - Single column on small screens
  - Three columns on medium and larger screens

- Each column:
  - Has a title
  - Displays a list of todo cards
  - Can grow vertically as todos are added

---

## Choosing the Layout Strategy

We will use **CSS Grid** for the main layout:

- Grid makes column-based layouts straightforward
- Responsive behavior is simple with Tailwind utilities
- Each column can internally use Flexbox for stacking todos

---

## Base Markup Structure

Inside `#outlet`, we will render the Kanban board.

```html
<div class="grid grid-cols-1 md:grid-cols-3 gap-4">
  <!-- To-Do column -->
  <!-- In-Progress column -->
  <!-- Done column -->
</div>
```

### Explanation

| Class            | Purpose                          |
| ---------------- | -------------------------------- |
| `grid`           | Enables CSS Grid                 |
| `grid-cols-1`    | Single column on small screens   |
| `md:grid-cols-3` | Three columns on medium+ screens |
| `gap-4`          | Space between columns            |

---

## Column Structure

Each column follows the same structure:

```html
<div class="bg-slate-100 rounded p-4">
  <h2 class="text-lg font-semibold mb-3">To-Do</h2>

  <div class="flex flex-col gap-2">
    <!-- Todo cards go here -->
  </div>
</div>
```

### Key Points

- Columns are visually separated using background color and padding
- Todos inside a column are stacked vertically using Flexbox
- `gap-2` provides consistent spacing between todo cards

---

## Rendering the Board (Initial Static Version)

For now, we will render a **static version** of the board to validate layout.

Create a file `src/todo/index.js` with the below content

Example:

```js
export function setupTodo() {
  document.querySelector("#outlet").innerHTML = `
     <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
   
       <div class="bg-slate-100 rounded p-4 min-h-[300px]">
         <h2 class="text-lg font-semibold mb-3">To-Do</h2>
         <div id="todo-list" class="flex flex-col gap-2"></div>
       </div>
   
       <div class="bg-slate-100 rounded p-4 min-h-[300px]">
         <h2 class="text-lg font-semibold mb-3">In-Progress</h2>
         <div id="in-progress-list" class="flex flex-col gap-2"></div>
       </div>
   
       <div class="bg-slate-100 rounded p-4 min-h-[300px]">
         <h2 class="text-lg font-semibold mb-3">Done</h2>
         <div id="done-list" class="flex flex-col gap-2 "></div>
       </div>
   
     </div>
   `;
}
```

Update `src/main.js` with the below content

```js
import { setupTodo } from "./todo/index.js";
import javascriptLogo from "./javascript.svg";
import "./style.css";
import lousingLogo from "/lousing-logo.svg";

document.querySelector("#app").innerHTML = `
  <div class="min-h-screen flex flex-col">

    <!-- Header -->
    <header class="sticky top-0 z-10 flex items-center px-6 py-4 border-b bg-[#242424]">
      <!-- Left logo -->
      <a href="https://github.com/neutral-00" target="_blank" class="logo flex items-center">
        <img src="${lousingLogo}" class="h-8 w-auto" alt="Lousing logo" />
      </a>

      <!-- Right group -->
      <div class="ml-auto flex items-center gap-4">
        <span class="text-lg font-semibold text-cyan-600 tracking-wide">
          Practice
        </span>

        <a
          href="https://developer.mozilla.org/en-US/docs/Web/JavaScript"
          target="_blank"
          class="flex items-center"
        >
          <img src="${javascriptLogo}" class="vanilla-js-logo h-8 w-auto" alt="JavaScript logo" />
        </a>
      </div>
    </header>

    <!-- Main content -->
    <main class="flex-1 p-6">
      <div id="outlet" class="max-w-6xl mx-auto"></div>
    </main>

  </div>
`;

setupTodo();
```

Next update `src/style.css` with the below content

```css
@import "tailwindcss";

:root {
  font-family: system-ui, Avenir, Helvetica, Arial, sans-serif;
  line-height: 1.5;
  font-weight: 400;

  color-scheme: light dark;
  color: darkcyan;
  background-color: #242424;

  font-synthesis: none;
  text-rendering: optimizeLegibility;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

a {
  font-weight: 500;
  color: #646cff;
  text-decoration: inherit;
}
a:hover {
  color: #535bf2;
}

body {
  margin: 0;
  /* display: flex; */
  /* place-items: center; */
  min-width: 320px;
  min-height: 100vh;
}

.logo:hover {
  filter: drop-shadow(0 0 2em oklch(60.9% 0.126 221.723));
}
.vanilla-js-logo:hover {
  filter: drop-shadow(0 0 2em #f7df1eaa);
}

.card {
  padding: 2em;
}

button {
  border-radius: 8px;
  border: 1px solid transparent;
  padding: 0.6em 1.2em;
  font-size: 1em;
  font-weight: 500;
  font-family: inherit;
  background-color: #1a1a1a;
  cursor: pointer;
  transition: border-color 0.25s;
}
button:hover {
  border-color: #646cff;
}
button:focus,
button:focus-visible {
  outline: 4px auto -webkit-focus-ring-color;
}

@media (prefers-color-scheme: light) {
  :root {
    color: #213547;
    background-color: #ffffff;
  }
  a:hover {
    color: #747bff;
  }
  button {
    background-color: #f9f9f9;
  }
}
```

> Note: For now, buttons use the default Vite styles.
> In later sections, we will replace these with Tailwind utility classes.

For simplicity, we are starting with a dark-themed layout.
Dark/light mode switching can be added later.

At this stage:

- No API calls are made
- No todos are rendered
- We are validating **layout and responsiveness only**

---

## Visual Result (Conceptual)

```
-----------------------------------------
|  To-Do  | In-Progress |     Done     |
|         |             |              |
|         |             |              |
-----------------------------------------
```

On small screens, these columns will stack vertically.

---

## Why Layout Comes First

Separating layout from logic helps us:

- Validate UI early
- Avoid mixing rendering logic with API calls
- Make the next steps easier to reason about

Once the layout is stable, we can focus on:

- Fetching data
- Rendering todo cards dynamically
- Handling user actions

---

### ✔️ End of Section

At this point:

- The Kanban layout is defined
- Tailwind Grid and Flexbox are working together
- The app has a clear visual structure

---

Perfect 👌
You’re doing this _exactly_ the right way. Let’s continue with the next section.

Below is **Section 5**, written in **ready-to-paste Markdown** for `20-todo-app.md`, consistent with everything you’ve built so far.

---

## Section 5 – Setting Up the Axios API Layer

In this section, we will create a **dedicated API layer** for communicating with the backend using **Axios**.

The goal is to:

- Centralize all API calls
- Keep network logic separate from UI logic
- Make the code easier to read, test, and extend

---

## Why a Dedicated API Layer?

Instead of calling Axios directly inside UI code, we isolate API logic into its own module.

Benefits:

- Cleaner UI code
- Single place to change API URLs or headers
- Easier error handling
- More realistic application structure

---

## API Base URL

Our JSON Server is running at:

```text
http://localhost:3300
```

And we have configured route rewriting so that all API endpoints are available under:

```text
http://localhost:3300/api
```

All Axios requests will use this base URL.

---

## Creating the API Module

Create a new file:

```text
src/todo/api.js
```

Add the following code:

```js
import axios from "axios";

const api = axios.create({
  baseURL: "http://localhost:3300/api",
  headers: {
    "Content-Type": "application/json",
  },
});

export function getTodos() {
  return api.get("/todos");
}

export function addTodo(todo) {
  return api.post("/todos", todo);
}

export function updateTodoStatus(id, status) {
  return api.patch(`/todos/${id}`, { status });
}

export function deleteTodo(id) {
  return api.delete(`/todos/${id}`);
}
```

---

## API Functions Overview

| Function           | Purpose                     |
| ------------------ | --------------------------- |
| `getTodos`         | Fetch all todos             |
| `addTodo`          | Create a new todo           |
| `updateTodoStatus` | Move a todo between columns |
| `deleteTodo`       | Remove a todo               |

Each function:

- Returns an Axios Promise
- Can be awaited by the caller
- Keeps API details hidden from UI logic

---

## Design Notes

### Why PATCH instead of PUT?

We use `PATCH` because:

- We are updating only the `status` field
- Partial updates are more efficient
- This reflects common real-world APIs

---

### Why return Axios Promises?

By returning the Axios call:

- UI code decides how to handle success or errors
- We keep the API layer flexible
- Async/await can be used naturally in callers

Example usage:

```js
const res = await getTodos();
console.log(res.data);
```

---

## No API Calls Yet (On Purpose)

At this stage:

- We are **not** calling the API from the UI
- No todos are rendered dynamically
- We are preparing the foundation

This keeps each section focused and easy to understand.

---

### ✔️ End of Section

At this point:

- Axios is configured correctly
- API functions are ready
- The app is prepared to fetch and modify todos

---

### 👉 Next Section

---

## Section 6 – Fetching and Rendering Todos

In this section, we will connect the **API layer** to the **UI layout**.

We will:

- Fetch todos from the backend
- Group them by status
- Render each todo in the correct column

At the end of this section, todos stored in JSON Server will appear on the screen.

---

## Rendering Strategy

We will follow this flow:

1. Fetch todos using the API layer
2. Group todos by status
3. Clear existing UI
4. Render each todo into its respective column

This keeps rendering logic predictable and easy to reason about.

---

## Importing API Functions

Update `src/todo/index.js` to import the API function:

```js
import { getTodos } from "./api.js";
```

---

## Fetching Todos

Inside `setupTodo`, we will fetch todos once the layout is rendered.

Update `setupTodo` as follows:

```js
import { getTodos } from "./api.js";

export async function setupTodo() {
  renderLayout();
  await loadTodos();
}
```

---

## Rendering the Layout (Refactor)

To keep responsibilities clear, extract layout rendering into its own function.

```js
function renderLayout() {
  document.querySelector("#outlet").innerHTML = `
    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">

      <div class="bg-slate-100 rounded p-4 min-h-[300px]">
        <h2 class="text-lg font-semibold mb-3">To-Do</h2>
        <div id="todo-list" class="flex flex-col gap-2"></div>
      </div>

      <div class="bg-slate-100 rounded p-4 min-h-[300px]">
        <h2 class="text-lg font-semibold mb-3">In-Progress</h2>
        <div id="in-progress-list" class="flex flex-col gap-2"></div>
      </div>

      <div class="bg-slate-100 rounded p-4 min-h-[300px]">
        <h2 class="text-lg font-semibold mb-3">Done</h2>
        <div id="done-list" class="flex flex-col gap-2"></div>
      </div>

    </div>
  `;
}
```

---

## Loading Todos from the API

Add the following function below `renderLayout`:

```js
async function loadTodos() {
  try {
    const res = await getTodos();
    renderTodos(res.data);
  } catch (error) {
    console.error("Failed to load todos", error);
  }
}
```

---

## Grouping Todos by Status

Before rendering, we group todos based on their status.

```js
function groupTodosByStatus(todos) {
  return {
    todo: todos.filter((t) => t.status === "todo"),
    inProgress: todos.filter((t) => t.status === "in-progress"),
    done: todos.filter((t) => t.status === "done"),
  };
}
```

---

## Rendering Todos into Columns

Add the render function:

```js
function renderTodos(todos) {
  const groups = groupTodosByStatus(todos);

  const todoList = document.getElementById("todo-list");
  const inProgressList = document.getElementById("in-progress-list");
  const doneList = document.getElementById("done-list");

  todoList.innerHTML = "";
  inProgressList.innerHTML = "";
  doneList.innerHTML = "";

  groups.todo.forEach((todo) => todoList.appendChild(createTodoCard(todo)));

  groups.inProgress.forEach((todo) =>
    inProgressList.appendChild(createTodoCard(todo)),
  );

  groups.done.forEach((todo) => doneList.appendChild(createTodoCard(todo)));
}
```

---

## Creating a Todo Card (Static Version)

For now, we render a **simple static card** without buttons.

```js
function createTodoCard(todo) {
  const div = document.createElement("div");
  div.className = "bg-white rounded px-3 py-2 shadow text-sm";

  div.textContent = todo.title;

  return div;
}
```

At this stage:

- Todos are displayed
- No actions are available yet
- The UI reflects backend data

---

## Why We Keep Cards Simple (For Now)

We intentionally avoid adding buttons here because:

- Rendering data first validates API integration
- UI behavior is easier to add incrementally
- Debugging becomes simpler

This step-by-step approach prevents tightly coupled logic.

---

### ✔️ End of Section

At this point:

- Todos are fetched from JSON Server
- Todos appear in the correct columns
- Layout + API + rendering are connected

---

### 👉 Next Section

Perfect 👍
Now that **layout, data fetching, and interactions** are solid, it’s time to complete the core workflow.

Below is **Section 8**, written cleanly for your tutorial.

---

## Section 8 – Adding New Todos

In this section, we will allow users to **add new tasks** to the board.

We will:

- Create a form for entering a new todo
- Persist the todo using the backend API
- Re-render the board after creation

This completes the **CRUD loop** for the Todo app.

---

## Todo Creation Requirements

A new todo should:

- Have a title entered by the user
- Default to `status: "todo"`
- Appear immediately in the **To-Do** column

---

## Adding the Todo Form

We will place the form **above the Kanban board**.

### Update `renderLayout`

Modify `renderLayout` in `src/todo/index.js`:

```js
function renderLayout() {
  document.querySelector("#outlet").innerHTML = `
    <div class="flex flex-col gap-6">

      <!-- Add Todo Form -->
      <form id="todo-form" class="flex gap-2 max-w-md">
        <input
          id="todo-input"
          type="text"
          placeholder="Add a new task..."
          class="flex-1 px-3 py-2 border rounded text-sm"
          required
        />
        <button
          type="submit"
          class="px-3 py-2 text-sm rounded bg-cyan-200 hover:bg-cyan-300 cursor-pointer"
        >
          Add
        </button>
      </form>

      <!-- Kanban Board -->
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
        <!-- columns unchanged -->
      </div>

    </div>
  `;
}
```

---

## Handling Form Submission

Add the following logic below `renderLayout`:

```js
import { createTodo } from "./api.js";
```

```js
function setupForm() {
  const form = document.getElementById("todo-form");
  const input = document.getElementById("todo-input");

  form.addEventListener("submit", async (e) => {
    e.preventDefault();

    const title = input.value.trim();
    if (!title) return;

    try {
      await createTodo({
        title,
        status: "todo",
      });

      input.value = "";
      await loadTodos();
    } catch (error) {
      console.error("Failed to create todo", error);
    }
  });
}
```

---

## Wiring It All Together

Update `setupTodo`:

```js
export async function setupTodo() {
  renderLayout();
  setupForm();
  await loadTodos();
}
```

---

## Why This Order Matters

We:

1. Render the layout
2. Attach form listeners
3. Fetch and render data

This ensures:

- DOM elements exist before event binding
- Data is always rendered last
- Side effects are predictable

---

## UX Improvements (Optional)

You can enhance UX with:

- Auto-focus input on load
- Disable button while submitting
- Show inline validation

These are intentionally left optional to keep the tutorial focused.

---

## Final Result

Users can now:

- Add new todos
- Move todos between columns
- See changes persisted instantly

This completes the **core functionality** of the Todo app.

---

### ✔️ End of Section

At this point, your app supports:

- Create
- Read
- Update

(Delete comes next.)

---

### 👉 Next Section

Awesome — this is the **final core CRUD action**.
We’ll keep it simple, safe, and consistent with everything you’ve already built.

Below is **Section 9**, ready to drop into `20-todo-app.md`.

---

## Section 9 – Deleting Todos

In this section, we will add the ability to **delete a todo**.

We will:

- Add a delete action to each todo card
- Remove the todo from the backend
- Refresh the UI after deletion

This completes the **CRUD cycle** for the Todo application.

---

## Deletion Strategy

We follow the same pattern used for moving todos:

1. Trigger an action from the UI
2. Call the backend API
3. Re-fetch and re-render todos

This ensures the UI always reflects the backend state.

---

## Adding Delete Support in the API Layer

In `src/todo/api.js`, add the following function if it doesn’t already exist:

```js
export function deleteTodo(id) {
  return api.delete(`/todos/${id}`);
}
```

---

## Adding a Delete Button to Todo Cards

We will add a small delete button to the right side of each card.

### Design Considerations

- Subtle and compact
- Visually distinct from move actions
- Uses color to indicate destructive action

---

## Updating `createTodoCard`

Update `createTodoCard` in `src/todo/index.js`:

```js
import { deleteTodo } from "./api.js";

function createTodoCard(todo) {
  const card = document.createElement("div");
  card.className =
    "bg-white rounded px-3 py-2 shadow-sm text-sm flex items-center gap-2";

  const title = document.createElement("span");
  title.className = "flex-1";
  title.textContent = todo.title;

  const actions = document.createElement("div");
  actions.className = "flex gap-2";

  if (todo.status !== "todo") {
    actions.appendChild(createActionButton("←", () => moveTodoLeft(todo)));
  }

  if (todo.status !== "done") {
    actions.appendChild(createActionButton("→", () => moveTodoRight(todo)));
  }

  const deleteBtn = document.createElement("button");
  deleteBtn.textContent = "✕";
  deleteBtn.className = `
    px-2 py-1
    text-xs font-medium
    rounded
    border border-red-300
    bg-red-200
    text-red-800
    hover:bg-red-300
    cursor-pointer
    transition
  `;
  deleteBtn.title = "Delete todo";
  deleteBtn.onclick = () => handleDelete(todo.id);

  actions.appendChild(deleteBtn);

  card.appendChild(title);
  card.appendChild(actions);

  return card;
}
```

---

## Handling Todo Deletion

Add the handler function below:

```js
async function handleDelete(id) {
  const confirmed = confirm("Delete this todo?");
  if (!confirmed) return;

  try {
    await deleteTodo(id);
    await loadTodos();
  } catch (error) {
    console.error("Failed to delete todo", error);
  }
}
```

---

## Why We Use Confirmation

Deletion is destructive.

A simple confirmation:

- Prevents accidental clicks
- Requires no additional UI
- Keeps the tutorial focused

---

## UX Result

Each todo card now has:

- Move left/right controls
- A small delete button (`✕`)

Clicking delete:

- Removes the todo from the backend
- Refreshes the board immediately

---

### ✔️ End of Section

At this point, your Todo app supports:

| Operation | Status |
| --------- | ------ |
| Create    | ✅     |
| Read      | ✅     |
| Update    | ✅     |
| Delete    | ✅     |

You now have a **complete CRUD application** built with vanilla JavaScript.

---
