
# JavaScript: Closures

A **closure** is created when a function "remembers" the variables from its outer scope, even after that scope has finished executing.

---

## 1. Definition & Examples

- A closure is the combination of a function and the lexical environment within which it was declared.
- Inner functions can access variables of outer functions even after the outer function has returned.

Example:
```js
function outer() {
  let count = 0;
  function inner() {
    count++;
    return count;
  }
  return inner;
}

const counter = outer();
console.log(counter()); // 1
console.log(counter()); // 2
console.log(counter()); // 3
```
Here, `inner` forms a closure over `count`.

---

## 2. Private Variables using Closures

- Variables in closures are not directly accessible from outside, useful for **encapsulation**.

Example:
```js
function createCounter() {
  let count = 0;
  return {
    increment: function() { count++; return count; },
    decrement: function() { count--; return count; },
    getCount: function() { return count; }
  };
}

const counter = createCounter();
console.log(counter.increment()); // 1
console.log(counter.getCount());  // 1
console.log(counter.decrement()); // 0
```
Here, `count` acts like a **private variable**.

---

## 3. Common Interview Patterns

### a) Function Factory
```js
function multiplier(factor) {
  return function(num) {
    return num * factor;
  };
}
const double = multiplier(2);
console.log(double(5)); // 10
```

### b) setTimeout Loop Issue
```js
for (var i = 1; i <= 3; i++) {
  setTimeout(() => console.log(i), 1000);
}
// Outputs: 4, 4, 4 (because `var` is function-scoped)
```

**Solution with `let` or closure:**
```js
for (let i = 1; i <= 3; i++) {
  setTimeout(() => console.log(i), 1000);
}
// Outputs: 1, 2, 3
```

### c) Once Function
```js
function once(fn) {
  let called = false;
  return function(...args) {
    if (!called) {
      called = true;
      return fn(...args);
    }
  };
}

const greetOnce = once(() => console.log("Hello!"));
greetOnce(); // "Hello!"
greetOnce(); // Nothing
```

---

**Summary Table:**

| Concept                   | Description                                           |
|---------------------------|-------------------------------------------------------|
| Closure                   | Function + lexical scope it remembers                 |
| Private Variables         | Data encapsulation using closures                     |
| Function Factory          | Returns functions with preserved outer variables      |
| setTimeout Loop Fix       | Use closures/`let` to capture loop variables correctly|
| Once Function             | Ensures a function runs only one time                 |
