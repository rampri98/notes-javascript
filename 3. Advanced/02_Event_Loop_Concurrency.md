
# JavaScript: Event Loop & Concurrency

JavaScript is single-threaded but uses the **event loop** to manage asynchronous operations, ensuring non-blocking behavior.

---

## 1. Callback Queue & Microtasks

- **Callback Queue (Task Queue)**: Stores callbacks from asynchronous APIs (`setTimeout`, `setInterval`).
- **Microtask Queue**: Stores promises (`.then`, `catch`, `finally`) and `MutationObserver` callbacks.
- Event Loop:
  1. Execute all tasks from the **call stack**.
  2. Process all **microtasks** before moving to the callback queue.

Example:
```js
console.log("start");

setTimeout(() => console.log("timeout"), 0);
Promise.resolve().then(() => console.log("promise"));

console.log("end");
// Output: start → end → promise → timeout
```

---

## 2. `setTimeout` and `setInterval`

- **setTimeout(fn, delay)** → Executes a function once after the given delay.
- **setInterval(fn, delay)** → Executes a function repeatedly at intervals.

Example:
```js
setTimeout(() => console.log("Runs once after 1s"), 1000);
setInterval(() => console.log("Runs every 2s"), 2000);
```

---

## 3. `requestAnimationFrame`

- Optimized for rendering animations at the browser’s refresh rate (~60 FPS).
- Runs before the next repaint, smoother than `setInterval` for animations.

Example:
```js
function animate() {
  console.log("Frame rendered");
  requestAnimationFrame(animate);
}
requestAnimationFrame(animate);
```

---

## 4. async/await & Event Loop

- `async/await` is built on top of Promises.
- `await` pauses function execution until the Promise resolves, but does not block the call stack.
- Resumed execution is scheduled as a **microtask**.

Example:
```js
async function demo() {
  console.log("1");
  await Promise.resolve();
  console.log("2");
}
demo();
console.log("3");
// Output: 1 → 3 → 2
```

---

**Summary Table:**

| Concept              | Role                                                                 |
|----------------------|----------------------------------------------------------------------|
| Call Stack           | Stores function execution contexts                                   |
| Callback Queue       | Stores tasks from async APIs (`setTimeout`, `setInterval`)           |
| Microtask Queue      | Stores promise callbacks (`.then`, `catch`, `finally`)               |
| setTimeout           | Runs a function once after a delay                                   |
| setInterval          | Runs a function repeatedly at intervals                              |
| requestAnimationFrame| Optimized for animations, runs before next repaint                   |
| async/await          | Uses promises, schedules continuation in microtask queue             |
