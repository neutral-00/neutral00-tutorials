# Closures

**Closures in JavaScript are functions that “remember” the variables from their outer scope, even after that outer function has finished executing.** They allow you to create private state and encapsulation, which is why they’re so powerful in JavaScript.

---

## 🔑 What is a Closure?

- A **closure** is formed when an inner function accesses variables defined in its outer function.
- Even after the outer function has returned, the inner function retains access to those variables.
- This is possible because of **lexical scoping**: functions in JavaScript carry their scope with them.

---

## Example - 1

````javascript
/*
CONCEPT: Closure
DEFINITION: A closure in JavaScript is a function bundled together with references to its surrounding state.

Example: In the below example, getInfo is a function that has access to properties of the outer function
usage:
```js
const { india } = require("./concepts/india");
let India = india();
console.log("population: " + India.population); // no direct access
console.log(India.getInfo());


// CLEANUP: Breaking the reference allows GC to reclaim memory
`India = null;`
Once you are done using the India object, set it to null.
This makes the closure and all its captured variables (name, area, states, population) eligible for garbage collection.
````

\*/

export function india() {
let name = "India";
let area = "3.287 million square kilometers";
let states = `28 states and 8 Union Territories`;
let population = "over 1.4 billion";
return {
getInfo: () => {
return `${name} has an area of ${area}. It has ${states}`;
},
};
}

````

## 📘 Simple Example

```javascript
function fruit(initialInventryCount, fruitName) {
  let count = initialInventryCount;
  let name = fruitName;

  return {
    getCount: () => count,
    getName: () => name,
    fillInventry: (n) => {
      if (typeof n === "number" && n > 0) {
        count += n;
      }
    },
    retrieveFromInventry: (n) => {
      if (typeof n === "number" && n > 0) {
        if (n <= count) {
          count -= n;
        } else {
          console.error("not enought supply in inventry");
        }
      }
    },
  };
}

let frutiStore1 = fruit(4, "apple");
console.log(frutiStore1.getName());
frutiStore1.fillInventry(2);
console.log("Balance in inventry: " + frutiStore1.getCount());
// another fruitStore
let frutiStore2 = fruit(12, "banana");
console.log(frutiStore2.getName());
frutiStore2.retrieveFromInventry(2);
console.log("Balance in inventry: " + frutiStore2.getCount());
````

### Explanation:

- Outer function defines two variables `name` and `count` returns an object containing inner functions.
- Even though the outer function has finished executing, inner functions still has access to the outer fields because of the closure.

---

## 📊 Key Benefits of Closures

| Benefit                | Example Use Case                      |
| ---------------------- | ------------------------------------- |
| **Data privacy**       | Hide variables from global scope      |
| **Encapsulation**      | Create modules with controlled access |
| **Stateful functions** | Counters, caches, memoization         |
| **Callbacks**          | Event handlers, async operations      |

---

## ⚠️ Things to Watch Out For

- **Memory leaks**: If closures hold onto large objects unnecessarily, they can prevent garbage collection.
- **Overuse**: Too many nested closures can make code harder to read and debug.

---

👉 In short: **Closures let functions carry their environment with them, enabling private state and powerful abstractions.** They’re one of the most important concepts to master in JavaScript.

---
