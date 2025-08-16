
# JavaScript: Asynchronous JS

JavaScript is single-threaded but supports asynchronous operations to handle tasks like network requests without blocking execution.

---

## 1. Callbacks

- A **callback** is a function passed as an argument to another function, executed later.
- Common in older APIs (e.g., `setTimeout`, event listeners).

Example:
```js
function fetchData(callback) {
  setTimeout(() => {
    callback("Data loaded");
  }, 1000);
}

fetchData((result) => {
  console.log(result);
});
```

**Drawback**: Callback Hell — deeply nested callbacks make code hard to read/maintain.

---

## 2. Promises

A Promise represents a value that may be available **now**, **later**, or **never**.

### Creating a Promise
```js
const promise = new Promise((resolve, reject) => {
  setTimeout(() => resolve("Success"), 1000);
});
```

### `.then()`, `.catch()`, `.finally()`
```js
promise
  .then((data) => console.log(data))      // Success
  .catch((error) => console.error(error)) // Handle error
  .finally(() => console.log("Done"));    // Always runs
```

---

### `Promise.all()`
- Resolves when **all** promises resolve, or rejects if any reject.
```js
Promise.all([
  Promise.resolve(1),
  Promise.resolve(2)
]).then(values => console.log(values)); // [1, 2]
```

### `Promise.race()`
- Resolves/rejects as soon as the **first** promise settles.
```js
Promise.race([
  new Promise(res => setTimeout(() => res("First"), 1000)),
  new Promise(res => setTimeout(() => res("Second"), 2000))
]).then(console.log); // "First"
```

---

## 3. async/await

- Syntactic sugar over Promises.
- `async` functions always return a Promise.
- `await` pauses execution until the Promise resolves/rejects.

Example:
```js
async function fetchData() {
  try {
    const result = await new Promise((resolve) => 
      setTimeout(() => resolve("Data loaded"), 1000)
    );
    console.log(result);
  } catch (error) {
    console.error(error);
  } finally {
    console.log("Done");
  }
}

fetchData();
```

---

**Summary Table:**

| Feature         | Purpose                                    | Pros                                    | Cons                      |
|-----------------|--------------------------------------------|-----------------------------------------|---------------------------|
| Callbacks       | Pass function to execute later              | Simple for small tasks                  | Callback hell, error handling messy |
| Promises        | Handle async results more cleanly           | Chainable, better error handling        | Still can get complex     |
| async/await     | Write async code like synchronous           | Readable, try/catch error handling      | Must be inside `async` function |
