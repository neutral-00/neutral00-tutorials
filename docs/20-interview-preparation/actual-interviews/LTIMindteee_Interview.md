# LTIMindtree FSD With Angular Interview Questions

Company: LTIMindtree
Position:  Java FSD with Angular
Date: 2025-09-19
Time: 12:00 - 12:45 PM IST

## CSS
Q. One CSS property is working in one browser but not in another, how would you fix it?
1. Use vendor prefixes (-webkit-, -moz-, -ms-, -o-)
```css
.element {
    -webkit-transform: scale(1.1);
    -moz-transform: scale(1.1);
    -ms-transform: scale(1.1);
    transform: scale(1.1);
}
```
1. Use CSS preprocessors or postprocessors like Autoprefixer
1. Check caniuse.com for browser compatibility

## Javascript

Q. code example for usage of bind and apply
```js
// bind example
const person = {
    name: 'John',
    greet: function(msg) {
        console.log(`${msg} ${this.name}!`);
    }
};

const employee = {
    name: 'Jane'
};

// Using bind
const boundGreet = person.greet.bind(employee);
boundGreet('Hello'); // Output: "Hello Jane!"

// Using apply
person.greet.apply(employee, ['Hi']); // Output: "Hi Jane!"

```
In JavaScript:

- **bind()** creates and returns a new function with a fixed `this` context and optional preset arguments but does not execute it immediately. The new function can be called later.
- **apply()** immediately calls the function with a given `this` context and accepts arguments as an array.
- The main difference between **apply()** and **bind()** is that `apply` invokes the function right away, while `bind` returns a new function to be invoked later.

Summary:
| Method | Usage                               | Arguments                    | Execution               |
|--------|-----------------------------------|-----------------------------|------------------------|
| bind() | Returns a new function with `this` bound | Arguments passed individually or preset | Deferred function call  |
| apply()| Calls function immediately with `this` bound | Arguments passed as array   | Immediate function call |

Both are used to explicitly set the `this` value inside functions.

Q. closures
A closure is a function that retains access to the variables of its outer (enclosing) function scope even after that outer function has returned. Closures are commonly used for data privacy and to create function factories.

Example:
```js
function makeCounter() {
    let count = 0; // private variable
    return function() {
        count += 1;
        return count;
    };
}

const counter = makeCounter();
console.log(counter()); // 1
console.log(counter()); // 2
```


Q. hoisting
Hoisting is JavaScript's behavior where variable and function declarations are conceptually moved to the top of their scope during the compilation phase. Important details:

- Function declarations are hoisted fully (you can call them before their definition).
- `var` declarations are hoisted but initialized to `undefined` until assignment.
- `let` and `const` are hoisted too but live in the Temporal Dead Zone (TDZ) until their declaration is evaluated; accessing them before initialization throws a ReferenceError.

```js
// var hoisting
console.log(x); // undefined
var x = 5;

// function hoisting
sayHello(); // "Hello"
function sayHello() { console.log('Hello'); }

// let/const and TDZ
console.log(y); // ReferenceError
let y = 5;
```

## angular

Q. Observables vs Promise
1. Observables can emit multiple values, Promises resolve once
1. Observables are lazy (need subscription), Promises execute immediately
1. Observables can be cancelled (unsubscribe), Promises cannot
1. Observables have operators for transformation and filtering
```ts
// Promise
const promise = new Promise(resolve => resolve('Hello'));
promise.then(value => console.log(value));

// Observable (RxJS)
import { Observable } from 'rxjs';
const observable = new Observable(subscriber => {
        subscriber.next('Hello');
        subscriber.next('World');
        subscriber.complete();
});
const subscription = observable.subscribe({
    next: v => console.log(v),
    complete: () => console.log('done')
});
subscription.unsubscribe();

Note: Promises execute the executor immediately when created; Observables only run when subscribed to.
```

Q. How to optimizes an angular app for performance?
1. Use OnPush Change Detection strategy
1. Lazy loading modules
1. Use trackBy for ngFor
1. Angular Universal for SSR
1. Minification and compression
1. Use pure pipes
1. Avoid memory leaks by unsubscribing
1. Use web workers for heavy computations
1. Enable production mode
1. Use AOT compilation

1. Prefer `trackBy` in `*ngFor` to reduce DOM churn




Q. write a code create a directive in angular
```ts
// Highlight directive
@Directive({
    selector: '[appHighlight]'
})
export class HighlightDirective {
    @Input() highlightColor: string;

    constructor(private el: ElementRef) {}

    @HostListener('mouseenter')
    onMouseEnter() {
        this.highlight(this.highlightColor || 'yellow');
    }

    @HostListener('mouseleave')
    onMouseLeave() {
        this.highlight(null);
    }

    private highlight(color: string) {
        this.el.nativeElement.style.backgroundColor = color;
    }
}

// Usage in template
<div appHighlight highlightColor="lightblue">
    This text will be highlighted
</div>
```

Q. Difference between pure and impure pipes?
- Pure pipes: Only execute when input value changes (by reference)
- Impure pipes: Execute on every change detection cycle
```ts
// Pure pipe (default)
@Pipe({
    name: 'myPure'
})
export class MyPurePipe implements PipeTransform {
    transform(value: any) { return value; }
}

// Impure pipe
@Pipe({
    name: 'myImpure',
    pure: false
})
export class MyImpurePipe implements PipeTransform {
    transform(value: any) { return value; }
}
```
- Impure pipes are useful for real-time filtering, sorting, or any dynamic updates where changes inside an object (mutations) need to trigger view updates. Use them sparingly — they run every change-detection cycle and can severely impact performance if overused.


Q. Tell about the different types of data binding in angular?
1. Interpolation: {{ expression }}
1. Property binding: [property]="value"
1. Event binding: (event)="handler()"
1. Two-way binding: [(ngModel)]="value"

Also note: `@Input()` and `@Output()` are the main decorators to implement property/event bindings between parent and child components.


## java
Q. You have a list of integers. Find the sum of even numbers using stream api without using the sum method?
```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);
int sumOfEven = numbers.stream()
    .filter(n -> n % 2 == 0)
    .reduce(0, (a, b) -> a + b);
// or
int sumOfEven = numbers.stream()
    .filter(n -> n % 2 == 0)
    .collect(Collectors.reducing(0, Integer::sum));
```

Q. How do you handle synchronosity in java?
Several mechanisms:
1. synchronized keyword
```java
public synchronized void method() { }
// or
synchronized(object) {
    // critical section
}
```
1. Lock interface
```java
private Lock lock = new ReentrantLock();
public void method() {
    lock.lock();
    try {
        // critical section
    } finally {
        lock.unlock();
    }
}
```
- ReentrantLock in Java is a class from the java.util.concurrent.locks package that implements the Lock interface
- providing more sophisticated locking than the traditional synchronized keyword.
- It allows the same thread to acquire the lock multiple times (reentrancy)

1. Atomic classes
```java
import java.util.concurrent.atomic.AtomicInteger;

class Counter extends Thread {
    private AtomicInteger count = new AtomicInteger(0);

    public void run() {
        for (int i = 0; i < 1000; i++) {
            count.incrementAndGet(); // Atomic increment
        }
    }

    public int getCount() {
        return count.get();
    }
}

public class AtomicExample {
    public static void main(String[] args) throws InterruptedException {
        Counter counter = new Counter();
        Thread t1 = new Thread(counter);
        Thread t2 = new Thread(counter);

        t1.start();
        t2.start();

        t1.join();
        t2.join();

        System.out.println("Count: " + counter.getCount()); // Consistent thread-safe count value
    }
}
```
- 
- Atomic classes are lock-free and suitable for high-performance multi-threading


Q. When will you use a list, map and queue?
- List: Ordered collection, when you need indexed access
- Map: Key-value pairs, when you need to associate values with unique keys
- Queue: FIFO operations, when you need ordered processing

Also consider specific implementations:
- `ArrayList` for fast random access; `LinkedList` for frequent insertions/removals at ends.
- `HashMap` for average O(1) lookups; `TreeMap` for sorted keys.
- `ArrayDeque` or `LinkedBlockingQueue` for producer-consumer scenarios.

Q. What is reflection? How is it useful?
Reflection allows examination/modification of class behavior at runtime

```java
// Example
Class<?> clazz = MyClass.class;
Method method = clazz.getDeclaredMethod("methodName", String.class);
Object instance = clazz.newInstance();
method.invoke(instance, "parameter");
```

Q. What is composition?
Composition is a design principle where a class is built using instances of other classes (has-a relationship) instead of inheriting from them (is-a). Composition favors reusability and loose coupling because it allows changing behavior at runtime by swapping composed objects.

Example:
```java
class Engine { void start() { /*...*/ } }
class Car {
    private final Engine engine;
    public Car(Engine engine) { this.engine = engine; }
    void start() { engine.start(); }
}
```

Use composition when you want to assemble behavior from multiple objects and avoid the fragility of deep inheritance hierarchies.

Q. How would you prevent thread deadlocks in java?
Common strategies to prevent and mitigate deadlocks:

- Consistent lock ordering: always acquire multiple locks in the same global order.
- Use lock timeouts: `tryLock(timeout, unit)` to back off instead of waiting indefinitely.
- Minimize lock scope: keep synchronized blocks as small as possible and avoid nested locks when feasible.
- Prefer higher-level concurrency utilities from `java.util.concurrent` (e.g., `ExecutorService`, `Semaphore`, `ConcurrentHashMap`) instead of manual locks.
- Deadlock detection and recovery: detect via thread dumps/monitoring and restart or release resources when possible.

Example using tryLock:
```java
if (lock.tryLock(500, TimeUnit.MILLISECONDS)) {
    try { /* critical section */ }
    finally { lock.unlock(); }
} else {
    // fallback or retry
}
```

Q. What is CompletableFuture?
`CompletableFuture` (Java 8+) is an implementation of `Future` that supports chaining and composition of asynchronous tasks with a fluent API. It allows non-blocking callback-style programming and combining multiple asynchronous results.

Key methods:
- `supplyAsync()` / `runAsync()` — start async tasks
- `thenApply()`, `thenAccept()`, `thenRun()` — chain dependent actions
- `thenCompose()` — flatten nested futures (for sequential async calls)
- `thenCombine()` — combine two independent futures
- `exceptionally()` / `handle()` — error handling
- `allOf()` / `anyOf()` — combine multiple futures

Example:
```java
CompletableFuture.supplyAsync(() -> fetchFromRemote())
    .thenApply(data -> transform(data))
    .thenAccept(result -> System.out.println(result))
    .exceptionally(ex -> { ex.printStackTrace(); return null; });
```


## system design

Q. How would you migrate a legacy monolithic  service to microservice?
High-level plan:

1. Inventory and domain decomposition: analyze the monolith, identify bounded contexts and service candidates.
2. Extract vertical slices: create small services that own their data and API boundaries.
3. API facade and strangler pattern: route traffic gradually to new services using an API gateway or routing layer.
4. Data migration: move from a single DB to per-service stores, keep data sync using events or the strangler pattern.
5. Observability & automation: add tracing, metrics, logging, and CI/CD for each service.
6. Operational changes: adopt containerization, service discovery, and orchestration (Kubernetes).

Start small (non-critical features) and iterate while keeping the monolith operational.

Q. How to design a realtime notification system?
High-level approach:

1. Requirements: define scale (messages/sec), latency SLO, persistence, and delivery guarantees (at-most-once, at-least-once, exactly-once).
2. Push channels: use WebSockets or Server-Sent Events (SSE) for browser clients; MQTT or platform push for mobile apps.
3. Message broker: use a scalable pub/sub system (Kafka, RabbitMQ, Redis Streams, or cloud pub/sub) for decoupling producers and consumers.
4. Fan-out: implement a notification service that subscribes to relevant events and fans out messages to connected clients. For large fan-out, partition recipients and distribute work across workers.
5. Connection management: maintain per-user connection metadata in a fast store (Redis) for routing messages to the right gateway node.
6. Persistence & retry: persist notifications for offline users and retry delivery when they reconnect; store durable logs for audit.
7. Security & rate-limiting: authenticate connections (JWT), authorize channels, and apply per-user rate-limits.

Example stack: Kafka (event backbone) + Java/Node notification workers + Redis for sessions + WebSocket gateway + CDN for static assets.

Q. How do you handle inter microservice communication?
Options and trade-offs:

- Synchronous HTTP/REST or gRPC for request-response interactions — simple but couples availability and latency.
- Asynchronous messaging (Kafka, RabbitMQ) for event-driven decoupling, higher resilience, and better scaling for high-throughput flows.
- API Gateway for authentication, routing, and protocol translation. Use service discovery for dynamic endpoints.
- Reliability patterns: implement timeouts, retries with exponential backoff, circuit breakers (resilience4j/Hystrix-like), and idempotency keys for safe retries.
- Monitoring and tracing: distributed tracing (OpenTelemetry), metrics, and logs to debug cross-service flows.

Prefer async events for decoupling and scalability; use sync calls for low-latency, strongly consistent operations.

Q. How to handle data consistency across distributed database systems?
Strategies:

- Choose a consistency model: strong consistency (transactions, 2PC) vs eventual consistency (events, CRDTs).
- Use the Saga pattern for long-running transactions: orchestrate or choreograph steps and compensate on failures.
- For critical operations, use distributed transactions carefully (2PC) — be mindful of performance and availability trade-offs.
- Event sourcing + CQRS: write events to an append-only log and build read models asynchronously to achieve eventual consistency.
- Use idempotent operations, ordered event delivery, and versioning to make retries safe and resolve conflicts deterministically.

Often a hybrid approach works best: strong consistency for critical operations (balances, settlements) and eventual consistency for analytics, caches, or denormalized views.

Q. How to design a finance system where realtime transactions are critical?
Key concerns: correctness, durability, low latency, atomicity, and auditability.

Design principles:

- Single source of truth: keep account balances in a strongly consistent store or a serialized transaction processor.
- Durable ledger: use append-only ledger for all transactions with replication for durability.
- Partitioning/sharding: shard by account/customer to scale throughput while keeping most transactions local to a shard.
- Use ACID transactions where necessary; for cross-shard transactions use Sagas with compensating actions.
- Strong observability and automated alerts for anomalies; include audit trails for regulatory compliance.
- Disaster recovery: regular backups, warm standbys, and well-tested failover procedures.

Example: transactional service (JVM) + PostgreSQL with partitioning or a distributed ledger + Kafka for event propagation + fast caches for reads with strict invalidation.

Q. How will you implement role based access using springboot and angular ?
High-level steps:

Backend (Spring Boot):
- Use Spring Security with JWT or session-based auth. Store users and roles in a database.
- Protect endpoints with method-level annotations (`@PreAuthorize("hasRole('ADMIN')")`) and URL-based rules in the security config.
- Include role claims in JWT and validate them server-side on each request.

Frontend (Angular):
- Store tokens securely (in-memory or httpOnly cookies); avoid localStorage if you can to reduce XSS risk.
- Decode JWT roles client-side to show/hide UI elements and guard routes with `CanActivate` guards.
- Attach `Authorization` header for API calls and handle 401/403 responses to redirect to login/forbidden pages.

Always enforce authorization on the server — client-side checks are only for UX.



## Database

Q. Write two sql queries one to fetch first and other to fetch last records from Employee table

Examples (MySQL / PostgreSQL / MariaDB):

```sql
-- Fetch first record (smallest ID)
SELECT * FROM Employee ORDER BY id ASC LIMIT 1;

-- Fetch last record (largest ID)
SELECT * FROM Employee ORDER BY id DESC LIMIT 1;
```

Examples (SQL Server):

```sql
-- Fetch first record
SELECT TOP 1 * FROM Employee ORDER BY id ASC;

-- Fetch last record
SELECT TOP 1 * FROM Employee ORDER BY id DESC;
```

Notes:
- Replace `id` with an appropriate ordering column (e.g., `created_at`) if you want first/last by insertion time or another criterion.
- For deterministic results, ensure `ORDER BY` uses a unique or at least consistent column.
- If you want first/last N records, use `LIMIT N` (MySQL/PostgreSQL) or `TOP N` (SQL Server).
