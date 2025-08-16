
# JavaScript Fundamentals – Interview Prep Notes

## 1. Variables
- Used to store data values.
- **Keywords**:
  - `var`: Function-scoped, can be re-declared, hoisted with `undefined`.
  - `let`: Block-scoped, cannot be re-declared in the same scope, hoisted but not initialized.
  - `const`: Block-scoped, cannot be re-assigned, must be initialized.

```javascript
var a = 10;
let b = 20;
const c = 30;
```

## 2. Data Types
### a. Primitive Types
- Stored directly in memory (immutable).
  - `Number` – e.g., `42`, `3.14`
  - `String` – e.g., `"Hello"`
  - `Boolean` – `true` or `false`
  - `null` – intentional absence of value
  - `undefined` – variable declared but not assigned
  - `Symbol` – unique and immutable identifier
  - `BigInt` – large integers beyond `Number` limits

```javascript
let num = 100;
let str = "JavaScript";
let flag = true;
let empty = null;
let notAssigned;
let id = Symbol("id");
let big = 123456789012345678901234567890n;
```

### b. Reference Types
- Stored as memory references (mutable).
  - `Object` – key-value pairs
  - `Array` – ordered list of values
  - `Function` – callable blocks of code

```javascript
let obj = { name: "Ramya", age: 26 };
let arr = [1, 2, 3];
function greet() { console.log("Hello"); }
```

## 3. Type Conversion
- **Implicit Conversion (Type Coercion)**: JS automatically converts types.
```javascript
"5" + 2    // "52" (String)
"5" - 2    // 3 (Number)
```
- **Explicit Conversion**: Manually convert types.
```javascript
Number("5");   // 5
String(5);     // "5"
Boolean(0);    // false
```

## 4. Operators
### a. Arithmetic Operators
- `+`, `-`, `*`, `/`, `%`, `**` (exponent)
```javascript
let x = 5 + 3; // 8
let y = 2 ** 3; // 8
```

### b. Assignment Operators
- `=`, `+=`, `-=`, `*=`, `/=`
```javascript
let a = 10;
a += 5; // 15
```

### c. Comparison Operators
- `==` vs `===`, `!=` vs `!==`, `<`, `>`, `<=`, `>=`
```javascript
5 == "5";  // true
5 === "5"; // false
```

### d. Logical Operators
- `&&` (AND), `||` (OR), `!` (NOT)
```javascript
true && false; // false
true || false; // true
!true;         // false
```

### e. Ternary Operator
- Short-hand if-else: `condition ? expr1 : expr2`
```javascript
let age = 18;
let status = age >= 18 ? "Adult" : "Minor";
```

### f. Nullish Coalescing `??`
- Returns right-hand side if left-hand side is `null` or `undefined`
```javascript
let username = null;
let name = username ?? "Guest"; // "Guest"
```

### g. Optional Chaining `?.`
- Safely access nested object properties
```javascript
let user = { profile: { email: "ramya@example.com" } };
let email = user.profile?.email; // "ramya@example.com"
let phone = user.profile?.phone; // undefined (no error)
```

## 5. Template Literals
- Use backticks `` ` `` for strings with embedded expressions
```javascript
let name = "Ramya";
let greeting = `Hello, ${name}!`; // "Hello, Ramya!"
```

## 6. Control Flow 
- Conditional Statements: if, else if, else, switch 
- Loops: for, while, do...while, for...of, for...in 
- break and continue

## 7. ES6 Features
- ES6 (ECMAScript 2015) introduced significant improvements to JavaScript syntax and functionality.
| Feature             | Benefit                                     |
|---------------------|---------------------------------------------|
| let/const           | Block scope, prevents accidental redeclare  |
| Template Literals   | Easier string building                      |
| Arrow Functions     | Shorter syntax, lexical `this`              |
| Destructuring       | Cleaner variable extraction                 |
| Spread/Rest         | Flexible data handling                      |
| Default Parameters  | Avoids `undefined` defaults                 |
| Modules             | Code organization, reusability              |