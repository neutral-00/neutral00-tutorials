# Lifecycle Hooks

From an interview perspective, it's crucial to not just list the lifecycle hooks but to explain **what they do**, **when they are called**, and **why they are important**. Think of it as explaining the "what," "when," and "why" for each one.

### The Lifecycle Hooks

An Angular component goes through a specific lifecycle, from its creation to its destruction. The lifecycle hooks are methods you can implement to tap into key moments during this process. They are called in a specific order:

| Hook                        | What it does                                                               | When is it called?                                                                                           | Why is it important?                                                                                                                                                                                                                          |
| :-------------------------- | :------------------------------------------------------------------------- | :----------------------------------------------------------------------------------------------------------- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **`ngOnChanges`**           | Detects changes to input properties.                                       | Called **before `ngOnInit`** and whenever one or more data-bound input properties change.                    | Useful for performing an action when an input value changes, especially if the action is complex and needs more than just a direct assignment.                                                                                                |
| **`ngOnInit`**              | Initializes the component and its data.                                    | Called **once** after the component's data-bound properties have been initialized for the first time.        | The most common hook. It's the ideal place for component initialization logic, such as fetching data from a server. It's preferred over the constructor for this purpose because the component's inputs are not available in the constructor. |
| **`ngDoCheck`**             | Detects and acts on changes that Angular can't or won't detect on its own. | Called immediately after `ngOnChanges` (on every change detection run).                                      | Used for custom change detection logic, like checking for changes in an object or a complex data structure. It's a performance-intensive hook and should be used with caution.                                                                |
| **`ngAfterContentInit`**    | Initializes the component's projected content.                             | Called **once** after Angular has fully initialized any content that is projected into the component's view. | Useful when you need to access or manipulate the content that is being passed from a parent component via `<ng-content>`.                                                                                                                     |
| **`ngAfterContentChecked`** | Detects changes in the projected content.                                  | Called after `ngAfterContentInit` and after every subsequent `ngDoCheck`.                                    | Used to perform additional change detection logic on the projected content.                                                                                                                                                                   |
| **`ngAfterViewInit`**       | Initializes the component's view and its child views.                      | Called **once** after Angular has fully initialized a component's view and its child views.                  | A crucial hook for accessing and manipulating **DOM elements** within the component's template, such as a `<div>` referenced with `@ViewChild`.                                                                                               |
| **`ngAfterViewChecked`**    | Detects changes in the component's view.                                   | Called after `ngAfterViewInit` and after every subsequent `ngAfterContentChecked`.                           | Used to perform additional change detection logic on the component's own view and its child views.                                                                                                                                            |
| **`ngOnDestroy`**           | Cleans up the component before it is destroyed.                            | Called **once**, just before the component is destroyed.                                                     | The most important hook for **preventing memory leaks**. It's the place to unsubscribe from observables, detach event handlers, or clear any intervals you may have set.                                                                      |

---

### The Interviewer's Perspective

When an interviewer asks about this, they're not just looking for a memorized list. They are often testing your understanding of:

- **Order of Execution:** Can you correctly state the order in which the hooks are called?
- **Purpose:** Do you know the specific use case for each hook?
- **Best Practices:** Do you know when to use `ngOnInit` versus the `constructor`? This is a very common follow-up question. The rule of thumb is: **constructor for dependency injection**, and **`ngOnInit` for component initialization logic**.
- **Performance:** Do you understand the performance implications of hooks like `ngDoCheck`? It shows you have a deeper understanding of the framework.
- **Memory Management:** Do you know that `ngOnDestroy` is vital for preventing memory leaks? This demonstrates good coding hygiene.
