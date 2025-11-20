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
A closure is a function that has access to variables in its outer (enclosing) scope, even after the outer function has returned.


Q. hoisting
Hoisting is JavaScript's default behavior of moving declarations to the top of their scope during compilation.
```js
// Variable hoisting
console.log(x); // undefined (not error)
var x = 5;

// Function hoisting
sayHello(); // "Hello" (works)
function sayHello() {
    console.log("Hello");
}

// Let and const are not hoisted
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

// Observable
const observable = new Observable(subscriber => {
    subscriber.next('Hello');
    subscriber.next('World');
});
const subscription = observable.subscribe(value => console.log(value));
subscription.unsubscribe();
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
- Impure pipes are useful for real-time filtering, sorting, or any dynamic updates where changes inside the object need to trigger updates in the view.
- overused can impact performance


Q. Tell about the different types of data binding in angular?
1. Interpolation: {{ expression }}
1. Property binding: [property]="value"
1. Event binding: (event)="handler()"
1. Two-way binding: [(ngModel)]="value"


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

Q. How would you prevent thread deadlocks in java?

Q. What is CompletableFuture?


## system design

Q. How would you migrate a legacy monolithic  service to microservice?

Q. How to design a realtime notification system?

Q. How do you handle inter microservice communication?

Q. How to handle data consistency accross distributed database systems

Q. How to design a finance system where realtime transactions are critical?

Q. How will you implement role based access using springboot and angular ?


## Database

Write two sql queries one to fetch first and other to fetch last records from Employee table
