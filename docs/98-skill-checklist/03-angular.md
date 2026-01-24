# Angular Skill Checklist

Here are list of must have skillsets a senior Angular Developer must have.
All these skills will be tested in a git repo: [https://github.com/neutral-00/poc-angular](https://github.com/neutral-00/poc-angular)
They will be group by branch name. For example, skills under `Components` will be tested under the git branch `components`.

## Components

### Core Components

1. [] @Component decorator basics
2. [] @Input() property binding
3. [] @Output() EventEmitter
4. [] @ViewChild() template reference
5. [] @ContentChild() content projection
6. [] @HostListener() DOM events
7. [] @HostBinding() host properties
8. [] ngOnInit() vs constructor()

### Lifecycle Hooks

9. [] ngOnChanges() input changes
10. [] ngOnDestroy() cleanup
11. [] OnInit/OnChanges interface
12. [] OnDestroy takeUntil pattern
13. [] ngAfterViewInit() ViewChildren

## Templates & Directives

### Template Syntax

1. [] \*ngIf structural directive
2. [] \*ngFor with trackBy
3. [] \*ngSwitch case/default
4. [] [ngClass] conditional classes
5. [] [ngStyle] dynamic styles
6. [] {{ interpolation }} pipes
7. [] async pipe subscription mgmt

### Structural Directives

8. [] custom \*ngIf with ng-template
9. [] @for (Angular 17+) syntax
10. [] @defer lazy loading blocks
11. [] ng-container optimization

### Attribute Directives

12. [] @Directive() host listeners
13. [] ElementRef nativeElement
14. [] Renderer2 safe DOM access
15. [] custom tooltip directive

## Services & Dependency Injection

### Services

1. [] @Injectable() providedIn: 'root'
2. [] constructor(private service: Type)
3. [] @Inject() custom tokens
4. [] InjectionToken creation
5. [] providedIn: 'platform' multi-app
6. [] factory providers functions

### HttpClient

7. [] HttpClientModule import
8. [] http.get() with typing
9. [] http.post() with body
10. [] interceptors HTTP_INTERCEPTORS
11. [] retry() errorStrategy
12. [] catchError() global handling

## Routing

### Core Routing

1. [] RouterModule.forRoot() routes
2. [] RouterLink / [routerLink]
3. [] router.navigate() programmatic
4. [] ActivatedRoute params
5. [] RouteResolver data loading
6. [] CanActivate guard auth

### Advanced Routing

7. [] lazy-loaded modules loadChildren
8. [] Router outlet animations
9. [] Route reuse strategy
10. [] PreloadingStrategy custom
11. [] CanDeactivate unsaved changes
12. [] RedirectCommand navigation

## State Management

### Signals (Angular 16+)

1. [] signal() writable signals
2. [] computed() derived signals
3. [] effect() side effects
4. [] toSignal() from RxJS
5. [] signalStore() Angular 18

### RxJS State

6. [] BehaviorSubject current value
7. [] Subject next() emit
8. [] shareReplay(1) caching
9. [] scan() accumulator state

## Forms

### Template-Driven

1. [] ngModel two-way binding
2. [] ngForm form validation
3. [] ngSubmit preventDefault

### Reactive Forms

4. [] FormBuilder group/controls
5. [] FormArray dynamic fields
6. [] Validators.required/custom
7. [] valueChanges subscription
8. [] markAsDirty() form state
9. [] AbstractControl patching

## Modules & Standalone

### NgModules

1. [] @NgModule declarations
2. [] exports vs imports
3. [] forRoot() static providers
4. [] Core/Shared module patterns

### Standalone Components

5. [] standalone: true components
6. [] import() in @Component
7. [] bootstrapApplication() no modules
8. [] provideRouter() standalone routing

## RxJS

### Creation Operators

1. [] of() from() static values
2. [] fromEvent() DOM events
3. [] interval() timer() scheduling
4. [] ajax() HttpClient alternative

### Transformation

5. [] map() pluck() projection
6. [] switchMap() cancel previous
7. [] concatMap() sequential
8. [] mergeMap() concurrent
9. [] exhaustMap() ignore new

### Utility

10. [] take() takeUntil() takeWhile()
11. [] debounceTime() distinctUntilChanged()
12. [] retry() retryWhen() backoff
13. [] catchError() global handler

## Testing

### Unit Tests

1. [] TestBed.configureTestingModule()
2. [] async() fakeAsync() tick()
3. [] ComponentFixture detectChanges()
4. [] DebugElement query()

### Angular Testing

5. [] HttpClientTestingModule
6. [] HttpTestingController expectOne()
7. [] RouterTestingModule harness
8. [] NO_ERRORS_SCHEMA bypass

## Performance

### Change Detection

1. [] OnPush strategy optimization
2. [] ChangeDetectorRef.markForCheck()
3. [] trackBy in \*ngFor
4. [] pure pipes memoization

### Build Optimization

5. [] ng build --prod aot
6. [] esbuild Angular 17+ speed
7. [] lazy loading routes
8. [] Bundle Analyzer webpack

## Angular 18+ Features

### Signals Everywhere

1. [] input() signal inputs
2. [] output() signal outputs
3. [] model() two-way signals
4. [] viewChild() signal queries

### Control Flow

5. [] @if @else @for blocks
6. [] @defer lazy rendering
7. [] @switch pattern matching

### Zoneless

8. [] destroyAfter signal lifecycle
9. [] provideExperimentalZonelessChangeDetection()
