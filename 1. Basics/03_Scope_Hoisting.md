
# JavaScript Scope & Hoisting – Interview Prep Notes

## 1. Global vs Local Scope
- **Global Scope**: Variables declared outside any function/block; accessible anywhere.
- **Local Scope**: Variables declared inside a function/block; accessible only within that function/block.

```javascript
let globalVar = "I am global";

function testScope() {
    let localVar = "I am local";
    console.log(globalVar); // Accessible
    console.log(localVar);  // Accessible
}

testScope();
console.log(globalVar); // Accessible
// console.log(localVar); // Error: not defined
```

## 2. Function Scope vs Block Scope
- **Function Scope**: Variables declared with `var` are function-scoped.
- **Block Scope**: Variables declared with `let` or `const` are block-scoped.

```javascript
function funcScope() {
    if (true) {
        var x = 10;      // Function scoped
        let y = 20;      // Block scoped
        const z = 30;    // Block scoped
    }
    console.log(x); // 10
    // console.log(y); // Error
    // console.log(z); // Error
}
funcScope();
```

## 3. Hoisting of `var`, `let`, `const`
- **Hoisting**: JS moves variable and function declarations to the top during compilation.
- `var` → hoisted and initialized as `undefined`.
- `let` & `const` → hoisted but **not initialized**; accessing before declaration causes ReferenceError.

```javascript
console.log(a); // undefined
var a = 5;

console.log(b); // ReferenceError
let b = 10;

console.log(c); // ReferenceError
const c = 15;
```

## 4. Lexical Environment
- **Definition**: Where a variable is physically declared in the source code.
- Functions have access to variables **lexically in their scope**, even if called elsewhere (closure concept).

```javascript
let globalVar = "Global";

function outer() {
    let outerVar = "Outer";

    function inner() {
        console.log(globalVar); // Accessible
        console.log(outerVar);  // Accessible
    }

    inner();
}
outer();
```