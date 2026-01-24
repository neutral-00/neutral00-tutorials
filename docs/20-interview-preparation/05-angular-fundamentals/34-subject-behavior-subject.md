# Subject Vs Behavior Subject

The primary difference between a `Subject` and a `BehaviorSubject` is how they handle the **last emitted value** for new subscribers.

  * A **`Subject`** doesn't retain the last value. New subscribers will only receive values that are emitted **after** they subscribe. It's a "fire-and-forget" model.
  * A **`BehaviorSubject`** always stores the last emitted value. When a new subscriber comes along, it **immediately receives the last value**, and then receives all subsequent values.

Think of it like a newspaper subscription. 📰

  * A **`Subject`** is like a standard subscription. If you sign up today, you'll start receiving tomorrow's paper, but you won't get a copy of all the previous issues.
  * A **`BehaviorSubject`** is like a subscription that includes the most recent issue. When you sign up, they send you yesterday's paper right away, and then you start receiving all the new ones as they're published.

-----

### Key Differences in Detail

| Feature | `Subject` | `BehaviorSubject` |
| :--- | :--- | :--- |
| **Initial Value** | Does **not** require an initial value. | **Requires** an initial value when created. |
| **Last Value** | Does **not** store the last emitted value. | **Stores** the last emitted value. |
| **New Subscribers** | Only receive **future** values. | Immediately receive the **last** value, then all future values. |
| **Common Use Case** | Event buses or simple event streams where you don't care about the history (e.g., a "click" event). | Managing application state, where new components need to know the current state as soon as they're initialized (e.g., a shopping cart total). |

### Code Examples

#### `Subject` Example

A new subscriber gets nothing at first, then gets the second value.

```typescript
import { Subject } from 'rxjs';

const subject = new Subject<number>();

subject.subscribe(value => console.log('Subscriber A:', value));

subject.next(1); // Subscriber A gets this

subject.subscribe(value => console.log('Subscriber B:', value));

subject.next(2); // Both Subscriber A and B get this
```

**Output:**

```
Subscriber A: 1
Subscriber A: 2
Subscriber B: 2
```

-----

#### `BehaviorSubject` Example

A new subscriber gets the initial value, then the second value.

```typescript
import { BehaviorSubject } from 'rxjs';

// Must be created with an initial value
const behaviorSubject = new BehaviorSubject<number>(0); 

behaviorSubject.subscribe(value => console.log('Subscriber A:', value));

behaviorSubject.next(1); // Subscriber A gets this

behaviorSubject.subscribe(value => console.log('Subscriber B:', value));

behaviorSubject.next(2); // Both Subscriber A and B get this
```

**Output:**

```
Subscriber A: 0  // Initial value
Subscriber A: 1
Subscriber B: 1  // Last value before subscription
Subscriber A: 2
Subscriber B: 2
```