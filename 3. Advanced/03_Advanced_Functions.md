
# JavaScript: Advanced Functions

Functions in JavaScript are **first-class citizens**, meaning they can be treated like values (assigned to variables, passed as arguments, or returned from functions). This allows advanced functional patterns.

---

## 1. IIFE (Immediately Invoked Function Expression)

- A function that runs immediately after it is defined.
- Useful for **creating private scopes** and avoiding global variable pollution.

Example:
```js
(function () {
  console.log("IIFE executed!");
})();

(() => {
  console.log("Arrow IIFE executed!");
})();
```

---

## 2. Function Currying

- Transforming a function with multiple arguments into a sequence of functions, each taking **one argument**.
- Helps with **partial application** and code reusability.

Example:
```js
function add(a) {
  return function(b) {
    return function(c) {
      return a + b + c;
    };
  };
}

console.log(add(1)(2)(3)); // 6

// ES6 arrow version
const multiply = a => b => c => a * b * c;
console.log(multiply(2)(3)(4)); // 24
```

---

## 3. Function Composition

- Combining multiple functions into one, where the output of one function becomes the input of the next.
- Used in **functional programming** for cleaner pipelines.

Example:
```js
const compose = (f, g) => x => f(g(x));

const double = x => x * 2;
const square = x => x * x;

const doubleThenSquare = compose(square, double);
console.log(doubleThenSquare(3)); // (3*2)^2 = 36
```

---

## 4. `bind`, `call`, `apply`

These methods are used to **control the value of `this`** inside functions.

- **call** → Invokes function with `this` and arguments passed individually.
- **apply** → Same as `call`, but arguments are passed as an array.
- **bind** → Returns a new function with `this` bound permanently.

Example:
```js
const person = { name: "Alice" };

function greet(greeting, punctuation) {
  console.log(greeting + ", " + this.name + punctuation);
}

greet.call(person, "Hello", "!");   // Hello, Alice!
greet.apply(person, ["Hi", "!!"]); // Hi, Alice!!

const boundGreet = greet.bind(person);
boundGreet("Hey", "...");           // Hey, Alice...
```

---

**Summary Table:**

| Concept    | Purpose                                              | Example                          |
|------------|------------------------------------------------------|----------------------------------|
| IIFE       | Execute function immediately, private scope          | `(function(){ ... })()`          |
| Currying   | Break down multi-arg fn into single-arg chain        | `add(1)(2)(3)`                   |
| Composition| Combine functions, pipeline of transformations       | `compose(square, double)(3)`     |
| call       | Invoke with explicit `this` & args list              | `fn.call(obj, arg1, arg2)`       |
| apply      | Invoke with explicit `this` & args array             | `fn.apply(obj, [arg1, arg2])`    |
| bind       | Permanently bind `this` and return new function      | `const fn2 = fn.bind(obj)`       |
