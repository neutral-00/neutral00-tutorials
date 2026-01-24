# Signals

Signals in angular are a system that granulary tracks how and where the state is used throughout the application.

Signal can be think of as a wrapper around a value.
The beauty is when that value changes consumers are notified.

A Signal is essesntially a getter function. When we call it, it returns the current value. Behind the sceens angular keeps track of which components or functions called that Signal, creating a dependency graph.


## Types
There are 3 types of Signals

1. Writable Signals
    - These are signals that we can update directly using the `set(value)` or `update(fn)`.
    - Set replaces the value
    - Update allows us to update a new value based on the current value.
    - Writable signals can be created using `signal()` function.

2. Computed Signals
    - They are readonly signals.
    - They derive their value from other signals.
    - If the source signal changes, the computed signal automatically recalculates
    - Lazy: They are evaluated only when actually read.

3. Effects
    - An effect is an operation that runs whenever or more signal values change.
    - They can be used for logging, syncing with locale storage or manual DOM manipulations.
    - You can not set other signals inside an effect. This is to prevent infinite loop.

