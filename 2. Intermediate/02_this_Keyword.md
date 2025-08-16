
# JavaScript: `this` Keyword

The `this` keyword refers to the **execution context** — the object that is currently calling the function.
Its value depends on **how** a function is invoked, not where it is defined.

---

## 1. Global Context

- In **non-strict mode**, `this` in the global scope refers to the global object:
  - In browsers → `window`
  - In Node.js → `global`
  ```js
  console.log(this); // window (in browser)
  ```

- In **strict mode**, `this` in the global scope is `undefined`:
  ```js
  'use strict';
  console.log(this); // undefined
  ```

---

## 2. Object Method Invocation

- When a function is called as a method of an object, `this` refers to that object.
  ```js
  const person = {
    name: "Alice",
    greet: function() {
      console.log(this.name);
    }
  };
  person.greet(); // "Alice"
  ```

- If the method is **extracted** and called separately, `this` may lose context:
  ```js
  const greetFn = person.greet;
  greetFn(); // undefined or error (depends on mode)
  ```

- **Solution**: Use `bind()` to fix `this`:
  ```js
  const boundGreet = person.greet.bind(person);
  boundGreet(); // "Alice"
  ```

---

## 3. Function Invocation

- In a regular function (not as a method), `this` refers to the global object (non-strict) or `undefined` (strict).
  ```js
  function showThis() {
    console.log(this);
  }
  showThis(); // window (non-strict), undefined (strict)
  ```

- In **event handlers** in browsers, `this` refers to the element that received the event:
  ```js
  document.querySelector("button").addEventListener("click", function() {
    console.log(this); // the button element
  });
  ```

---

## 4. Arrow Functions vs Regular Functions

- **Arrow functions** do **not** have their own `this`.  
  They inherit `this` from their surrounding **lexical scope**.
  ```js
  const obj = {
    name: "Alice",
    arrowGreet: () => console.log(this.name),
    regularGreet: function() { console.log(this.name); }
  };
  
  obj.arrowGreet(); // undefined (inherits from global scope)
  obj.regularGreet(); // "Alice"
  ```

- Common use case: Keep `this` inside callbacks
  ```js
  function Person(name) {
    this.name = name;
    setTimeout(() => {
      console.log(this.name); // works, inherits from Person context
    }, 1000);
  }
  new Person("Alice");
  ```
