# JavaScript: Modules & Bundlers

Modules help structure code into reusable pieces. Bundlers optimize and prepare modules for browsers.

---

## 1. ES Modules vs CommonJS

### ES Modules (ESM)
- Standardized in ES6.
- Uses ```import``` and ```export``` keywords.
- Static analysis → can be optimized by bundlers (e.g., tree-shaking).
- Runs in strict mode by default.
- Browser & modern Node.js support.

Example:
```js
// math.js
export const add = (a, b) => a + b;

// main.js
import { add } from "./math.js";
console.log(add(2, 3));
```

### CommonJS (CJS)
- Used in Node.js (before ESM support).
- Uses ```require``` and ```module.exports```.
- Synchronous loading (not suitable for browsers without bundling).
- Dynamically evaluated.

Example:
```js
// math.js
module.exports.add = (a, b) => a + b;

// main.js
const { add } = require("./math");
console.log(add(2, 3));
```

**Key Differences:**
| Feature       | ES Modules (ESM)        | CommonJS (CJS)           |
|---------------|--------------------------|--------------------------|
| Syntax        | ```import/export```          | ```require/module.exports``` |
| Loading       | Static (compile-time)    | Dynamic (runtime)        |
| Scope         | Strict mode by default   | Non-strict (by default)  |
| Environment   | Browser + Node.js (new) | Node.js (legacy)         |

---

## 2. Dynamic Imports

- Allows **lazy loading** of modules.
- Syntax: ```import()``` returns a **Promise**.
- Useful for code-splitting & conditional loading.

Example:
```js
async function loadModule() {
  const module = await import("./math.js");
  console.log(module.add(2, 5));
}
loadModule();
```

---

## 3. Tree Shaking Basics

- **Tree shaking** = Removing unused code during bundling.
- Relies on ES Modules' **static structure**.
- Bundlers like **Webpack, Rollup, Parcel, ESBuild** support it.
- Only works with ESM (not CJS).

Example:
```js
// utils.js
export function used() { console.log("I am used"); }
export function unused() { console.log("I am unused"); }

// main.js
import { used } from "./utils.js";
used();
```
// In final bundle, ```unused()``` will be removed by tree shaking.

---

## Summary Table

| Concept         | Purpose                               | Example                        |
|-----------------|---------------------------------------|--------------------------------|
| ES Modules (ESM)| Modern, static imports/exports        | ```import { add } from "..."```    |
| CommonJS (CJS)  | Node.js legacy module system          | ```const x = require("...")```     |
| Dynamic Imports | Lazy load modules at runtime          | ```const m = await import("...")```|
| Tree Shaking    | Remove unused exports during bundling | ```export unused() {...}``` (removed) |
