
# JavaScript Functions – Interview Prep Notes

## 1. Function Declaration vs Function Expression

### a. Function Declaration
- Named function, hoisted (can be called before definition).
```javascript
console.log(greet("Ramya")); // Hello, Ramya
function greet(name) {
    return `Hello, ${name}`;
}
```

### b. Function Expression
- Function assigned to a variable, not hoisted.
```javascript
console.log(greet("Ramya")); // ReferenceError
const greet = function(name) {
    return `Hello, ${name}`;
};
```

## 2. Arrow Functions
- Shorter syntax, **does not have its own `this`**.
```javascript
const greet = (name) => `Hello, ${name}`;
console.log(greet("Ramya")); // Hello, Ramya

// With multiple parameters
const add = (a, b) => a + b;
console.log(add(2, 3)); // 5
```

## 3. Default Parameters
- Provide default values if arguments are missing.
```javascript
function greet(name = "Guest") {
    return `Hello, ${name}`;
}
console.log(greet()); // Hello, Guest
```

## 4. Rest Parameters `(...args)`
- Collects multiple arguments into an array.
```javascript
function sum(...numbers) {
    return numbers.reduce((acc, curr) => acc + curr, 0);
}
console.log(sum(1, 2, 3, 4)); // 10
```

## 5. `return` Statement
- Returns a value from the function. If omitted, function returns `undefined`.
```javascript
function multiply(a, b) {
    return a * b;
}
console.log(multiply(2, 3)); // 6

function noReturn() {
    console.log("Hello");
}
console.log(noReturn()); // undefined
```
## 6. Modules: `import` / `export`

- **Export**:
```js
// file: math.js
export const add = (a, b) => a + b;
export default function multiply(a, b) {
  return a * b;
}
```

- **Import**:
```js
import multiply, { add } from './math.js';
```