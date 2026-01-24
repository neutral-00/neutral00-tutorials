# Learning Roadmap ✅

This syllabus provides a structured, modern roadmap for mastering Angular 21, Signals, Zoneless apps, and scalable architecture. It is designed for teams, training programs, and self‑paced learning.

---

### **1. Project Setup & Tooling**

- [x] 1.1 Angular CLI fundamentals
- [x] 1.2 Standalone app setup
- [x] 1.3 Workspace structure (apps + libraries)
- [x] 1.4 Strict mode & TypeScript config
- [x] 1.5 Environment management
- [x] 1.6 Linting, formatting, testing setup
- [x] 1.7 Angular version updates

---

### **2. Components & Architecture**

- [x] 2.1 Standalone components
- [ ] 2.2 Inputs & outputs
- [ ] 2.3 Component communication patterns
- [ ] 2.4 Lifecycle hooks
- [ ] 2.5 View queries (classic + signals)
- [ ] 2.6 Smart vs. presentational components

---

### **3. Template Syntax & Rendering**

- [ ] 3.1 Interpolation & bindings
- [ ] 3.2 Structural directives
- [ ] 3.3 Modern control flow (`@if`, `@for`, `@switch`)
- [ ] 3.4 Template reference variables
- [ ] 3.5 Rendering performance

---

### **4. Directives**

- [ ] 4.1 Built‑in attribute directives
- [ ] 4.2 Custom attribute directives
- [ ] 4.3 HostBinding & HostListener
- [ ] 4.4 Custom structural directives
- [ ] 4.5 Directive vs. component decision‑making

---

### **5. Pipes**

- [ ] 5.1 Built‑in pipes
- [ ] 5.2 Pure vs. impure pipes
- [ ] 5.3 Custom pipes
- [ ] 5.4 Pipe performance

---

### **6. Styling & UI Architecture**

- [ ] 6.1 Component‑scoped styles
- [ ] 6.2 SCSS architecture
- [ ] 6.3 CSS custom properties
- [ ] 6.4 Angular Material theming
- [ ] 6.5 Global design system

---

### **7. Forms**

- [ ] 7.1 Template‑driven forms
- [ ] 7.2 Reactive Forms
- [ ] 7.3 FormBuilder & FormArray
- [ ] 7.4 Sync + async validation
- [ ] 7.5 Form state management

---

### **8. Services & Dependency Injection**

- [ ] 8.1 Injectable services
- [ ] 8.2 DI scopes (`root`, `platform`, `any`)
- [ ] 8.3 HttpClient usage
- [ ] 8.4 InjectionToken & custom providers
- [ ] 8.5 Factory & multi providers

---

### **9. Routing & Navigation**

- [ ] 9.1 Standalone routing
- [ ] 9.2 Route params & query params
- [ ] 9.3 Guards & resolvers
- [ ] 9.4 Lazy loading & preloading
- [ ] 9.5 Route animations

---

### **10. Signals (Angular 17–21)**

- [ ] 10.1 Writable & computed signals
- [ ] 10.2 Effects
- [ ] 10.3 `toSignal` conversions
- [ ] 10.4 Signal inputs/outputs
- [ ] 10.5 Signal Store
- [ ] 10.6 Signals vs. RxJS

---

### **11. HTTP & Interceptors**

- [ ] 11.1 HttpClient configuration
- [ ] 11.2 Functional interceptors
- [ ] 11.3 Auth, caching, retry patterns
- [ ] 11.4 API abstraction

---

### **12. Testing**

- [ ] 12.1 Component testing
- [ ] 12.2 DOM testing
- [ ] 12.3 HttpClientTestingModule
- [ ] 12.4 RouterTestingHarness
- [ ] 12.5 Mocking strategies

---

### **13. Performance Optimization**

- [ ] 13.1 OnPush & zoneless
- [ ] 13.2 TrackBy & memoization
- [ ] 13.3 Pure pipes
- [ ] 13.4 Lazy loading
- [ ] 13.5 Bundle analysis

---

### **14. Angular 21 Features**

- [ ] 14.1 New control flow blocks
- [ ] 14.2 `@defer`
- [ ] 14.3 Zoneless change detection
- [ ] 14.4 Enhanced signals (`resource`, `query`)
- [ ] 14.5 Server‑side signals

---

### **15. State Management**

- [ ] 15.1 Signal Store
- [ ] 15.2 State + computed + methods
- [ ] 15.3 NgRx (optional)
- [ ] 15.4 Choosing the right state strategy

---

### **16. Deployment & DevOps**

- [ ] 16.1 Production builds
- [ ] 16.2 Dockerization
- [ ] 16.3 Nginx SPA config
- [ ] 16.4 CI/CD pipelines
- [ ] 16.5 PWA setup

---

## **ASCII Roadmap Diagram**

```
Angular 21 Roadmap
│
├── 1. Setup & Tooling
│
├── 2. Components & Architecture
│
├── 3. Template Syntax & Rendering
│
├── 4. Directives
│
├── 5. Pipes
│
├── 6. Styling & UI Architecture
│
├── 7. Forms
│
├── 8. Services & DI
│
├── 9. Routing & Navigation
│
├── 10. Signals (17–21)
│
├── 11. HTTP & Interceptors
│
├── 12. Testing
│
├── 13. Performance Optimization
│
├── 14. Angular 21 Features
│
├── 15. State Management
│
└── 16. Deployment & DevOps
```

---

# ✅ 3. Branch Naming Strategy (Aligned With High‑Level Roadmap)

Use a **prefix + number + slug** format:

```
<category>/<sequence>-<topic>
```

### ✅ Categories

1. `setup`
1. `components`
1. `templates`
1. `directives`
1. `pipes`
1. `styling`
1. `forms`
1. `services`
1. `routing`
1. `signals`
1. `http`
1. `testing`
1. `performance`
1. `angular21`
1. `state`
1. `deployment`

### ✅ Examples

```
01-setup/1-cli-basics
02-components/1-standalone-components
03-templates/1-control-flow
04-directives/1-custom-structural
05-pipes/1-custom-pipes
06-styling/1-material-theming
07-forms/reactive-forms
08-services/1-di-tokens
09-routing/1-lazy-loading
10-signals/1-signal-store
11-http/1-functional-interceptors
12-testing/1-router-testing
13-performance/1-onpush
14-angular21/1-defer-blocks
15-state/1-ngrx-effects
16-deployment/1-docker-nginx
```

---

```
# Angular 21 Learning Roadmap - Low Level

Master Angular 21 step by step with 200+ granular concepts.
All concepts demoed in git repo: [https://github.com/neutral-00/practice-angular](https://github.com/neutral-00/practice-angular)
Grouped by branch name (e.g., `components-1-1` for Components > 1.1).

## 1. Setup & CLI (branch: `setup`)

### Project Setup

1.1 [] `ng new app --standalone --routing --style=scss`
1.2 [] `ng generate application sub-app`
1.3 [] `ng serve --port 4201 --open`
1.4 [] `ng build --prod --base-href=/app/`
1.5 [] `ng generate component hero --standalone`

### CLI Advanced

1.6 [] `ng generate library ui-kit`
1.7 [] `ng config strictTemplates true`
1.8 [] `ng update @angular/core@21`
1.9 [] `ng lint --fix`
1.10 [] `ng test --code-coverage`

## 2. Components (branch: `components-*`)

### Core Components

2.1 [] `@Component({ selector: 'app-hero', standalone: true })`
2.2 [] `template: '<h1>{{title}}</h1>'` inline template
2.3 [] `templateUrl: './hero.component.html'` external
2.4 [] `styles: ['h1 { color: blue; }']` inline styles
2.5 [] `styleUrls: ['./hero.component.scss']` external SCSS

### Inputs & Outputs

2.6 [] `@Input() heroName: string = ''`
2.7 [] `@Output() heroSelected = new EventEmitter<Hero>()`
2.8 [] `heroSelected.emit(hero)`
2.9 [] `@Input({ required: true }) title!: string` Angular 17+

### Lifecycle Hooks

2.10 [] `ngOnInit()` initialization
2.11 [] `ngOnChanges(changes: SimpleChanges)` input changes
2.12 [] `ngOnDestroy()` cleanup subscriptions
2.13 [] `ngAfterViewInit()` view children ready
2.14 [] `OnInit, OnDestroy` interfaces

### View/Query

2.15 [] `@ViewChild(HeroComponent)` single child
2.16 [] `@ViewChildren(HeroComponent) heroes!: QueryList<HeroComponent>`
2.17 [] `@ViewChild('heroForm', { static: true }) form!: ElementRef`
2.18 [] `viewChild(HeroComponent)` signal (Angular 17+)

## 3. Template Syntax (branch: `templates-*`)

### Interpolation & Property Binding

3.1 [] `{{ hero.name }}` interpolation
3.2 [] `[id]="hero.id"` property binding
3.3 [] `[hidden]="!hero.name"` boolean attributes
3.4 [] `[attr.aria-label]="hero.description"` attributes

### Event Binding

3.5 [] `(click)="onSelect(hero)"` DOM events
3.6 [] `(ngModelChange)="onNameChange($event)"` Angular events
3.7 [] `($event)"` event object access

### Structural Directives

3.8 [] `*ngIf="hero"` conditional rendering
3.9 [] `*ngFor="let hero of heroes; trackBy: trackById"`
3.10 [] `*ngSwitchCase="hero.type"` switch
3.11 [] `@for (hero of heroes; track hero.id)` Angular 17+
3.12 [] `@if (hero.active); else inactiveTpl` Angular 17+

## 4. Directives (branch: `directives-*`)

### Built-in Attribute Directives

4.1 [] `[ngClass]="{ active: hero.active }"`
4.2 [] `[ngStyle]="{ background: hero.color }"`
4.3 [] `[ngModel]="hero.name"` two-way binding

### Custom Structural Directives

4.4 [] `@Directive({ selector: '[appUnless]' })` unless directive
4.5 [] `TemplateRef` and `ViewContainerRef`
4.6 [] `viewContainer.createEmbeddedView(templateRef)`

### Custom Attribute Directives

4.7 [] `@Directive({ selector: '[appHighlight]' })`
4.8 [] `@HostListener('mouseenter') onMouseEnter()`
4.9 [] `@HostBinding('style.backgroundColor') bgColor! = ''`
4.10 [] `ElementRef` and `Renderer2`

## 5. Pipes (branch: `pipes-*`)

### Built-in Pipes

5.1 [] `{{ hero.birthday | date:'medium' }}`
5.2 [] `{{ heroes | json }}`
5.3 [] `{{ value | async }}` observables
5.4 [] `{{ text | uppercase | titlecase }}` chaining

### Custom Pipes

5.5 [] `@Pipe({ name: 'duration', standalone: true })`
5.6 [] `transform(value: number): string`
5.7 [] `pure: false` impure pipe
5.8 [] `@Pipe({ pure: false })` impure performance

## 6. Styling (branch: `styling-*`)

### Component Styles

6.1 [] `styleUrls: ['./hero.component.scss']`
6.2 [] `:host { display: block; }` host selector
6.3 [] `::ng-deep .external-class { color: red; }`
6.4 [] `ViewEncapsulation.None` global styles

### Dynamic Styling

6.5 [] `[class.active]="hero.active"`
6.6 [] `[ngClass]="'hero-card hero-' + hero.type"`
6.7 [] `[style.font-size.px]="hero.level * 10"`

### Theming

6.8 [] SCSS variables `$primary-color: #1976d2`
6.9 [] CSS custom properties `--primary-color`
6.10 [] Angular Material theme integration

## 7. Forms (branch: `forms-*`)

### Template-driven Forms

7.1 [] `[(ngModel)]="hero.name"` two-way binding
7.2 [] `ngForm` form validation
7.3 [] `ngSubmit="onSubmit()"` form submit

### Reactive Forms

7.4 [] `FormBuilder.group({ name: ['', Validators.required] })`
7.5 [] `FormArray` dynamic form arrays
7.6 [] `form.valueChanges` subscribe changes
7.7 [] `CustomValidator` async validators
7.8 [] `markAsDirty()` form state control

## 8. Services & DI (branch: `services-*`)

### Services

8.1 [] `@Injectable({ providedIn: 'root' })`
8.2 [] `constructor(private http: HttpClient)`
8.3 [] `@Inject(HEROES)` custom tokens

### Dependency Injection

8.4 [] `providedIn: 'platform'` multi-app
8.5 [] `useFactory` factory providers
8.6 [] `useExisting` alias providers
8.7 [] `InjectionToken` custom tokens

## 9. Routing (branch: `routing-*`)

### Basic Routing

9.1 [] `provideRouter(routes)` standalone
9.2 [] `{ path: 'hero/:id', component: HeroDetailComponent }`
9.3 [] `<a routerLink="/hero/{{hero.id}}">Hero</a>`
9.4 [] `ActivatedRoute.snapshot.paramMap`

### Advanced Routing

9.5 [] `loadChildren: () => import('./heroes/heroes.routes').then(m => m.HEROES_ROUTES)`
9.6 [] `CanActivate` route guards
9.7 [] `CanDeactivate` unsaved changes
9.8 [] `Resolve` route data loading
9.9 [] `PreloadingStrategy` eager/lazy
9.10 [] Route animations

## 10. Signals (Angular 17+) (branch: `signals-*`)

### Core Signals

10.1 [] `signal(0)` writable signals
10.2 [] `computed(() => count() * 2)` derived
10.3 [] `effect(() => console.log(count()))` side effects
10.4 [] `toSignal(obs$)` from RxJS

### Component Signals

10.5 [] `input.required()` signal inputs
10.6 [] `output()` signal outputs
10.7 [] `model()` two-way binding
10.8 [] `viewChild()` signal queries
10.9 [] `signalStore()` state management

## 11. HTTP Client (branch: `http-*`)

### HttpClient Setup

11.1 [] `provideHttpClient(withInterceptors())`
11.2 [] `http.get<Hero[]>('/api/heroes')`
11.3 [] `http.post<Hero>('/api/heroes', hero)`

### Interceptors

11.4 [] Functional interceptor `HttpInterceptorFn`
11.5 [] `withInterceptors([authInterceptor])`
11.6 [] Class-based `implements HttpInterceptor`
11.7 [] `HTTP_INTERCEPTORS` multi provider

## 12. Testing (branch: `testing-*`)

### Unit Tests

12.1 [] `TestBed.createComponent(HeroComponent)`
12.2 [] `fixture.detectChanges()`
12.3 [] `fixture.nativeElement.querySelector()`
12.4 [] `async()` fakeAsync testing

### Angular Testing

12.5 [] `HttpClientTestingModule`
12.6 [] `HttpTestingController.expectOne()`
12.7 [] `RouterTestingHarness`
12.8 [] `NO_ERRORS_SCHEMA`

## 13. Performance (branch: `performance-*`)

### Change Detection

13.1 [] `ChangeDetectionStrategy.OnPush`
13.2 [] `ChangeDetectorRef.markForCheck()`
13.3 [] `trackBy` function in `*ngFor`
13.4 [] `pure` pipe optimization

### Build Optimization

13.5 [] `ng build --prod` AOT compilation
13.6 [] Lazy loading modules/routes
13.7 [] Bundle analyzer webpack
13.8 [] Tree shaking unused code

## 14. Angular 21 Features (branch: `angular21-*`)

### Control Flow

14.1 [] `@if (condition) { ... } @else { ... }`
14.2 [] `@for (item of items; track item.id) { ... }`
14.3 [] `@switch (value) { @case (1) ... }`
14.4 [] `@defer (on viewport) { ... }`

### Zoneless (Experimental)

14.5 [] `provideExperimentalZonelessChangeDetection()`
14.6 [] `destroyRef()` signal lifecycle

### Enhanced Signals

14.7 [] `resource()` data fetching signals
14.8 [] `query()` server-side signals

## 15. State Management (branch: `state-*`)

### Signals Store

15.1 [] `signalStore()` feature state
15.2 [] `withMethods()`, `withComputed()`
15.3 [] `withState()`, `patchState()`

### NgRx (Optional)

15.4 [] `@ngrx/store` actions/reducers
15.5 [] `@ngrx/effects` side effects
15.6 [] `createEffect()` async actions

## 16. Deployment (branch: `deployment-*`)

16.1 [] `ng build --prod --output-path=dist`
16.2 [] Docker multi-stage build
16.3 [] Nginx configuration
16.4 [] Environment-specific builds
16.5 [] Progressive Web App (PWA)
```
