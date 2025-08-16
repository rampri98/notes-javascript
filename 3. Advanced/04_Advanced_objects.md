# JavaScript: Advanced Objects

JavaScript objects provide advanced features for controlling property behavior, immutability, and custom iteration.

---

## 1. Object Descriptors: writable, configurable, enumerable

- Each object property has a **descriptor** controlling its behavior.

**Property Descriptor Attributes:**
- **writable** → If false, property cannot be modified.
- **configurable** → If false, property cannot be deleted or reconfigured.
- **enumerable** → If false, property won't appear in loops (```for...in```, ```Object.keys```).

Example:

```js
const obj = {};
Object.defineProperty(obj, "name", {
  value: "Alice",
  writable: false,
  configurable: false,
  enumerable: true
});

console.log(obj.name); // Alice
obj.name = "Bob";      // Error in strict mode, ignored otherwise
console.log(Object.keys(obj)); // ["name"]
```

---

## 2. Object.freeze() & Object.seal()

- **Object.freeze(obj)** → Makes the object completely **immutable** (cannot add, delete, or modify properties).
- **Object.seal(obj)** → Prevents adding or deleting properties, but allows modifying existing ones.

Example:

```js
const user = { name: "Alice" };

Object.freeze(user);
user.name = "Bob"; // Ignored
console.log(user.name); // Alice

const person = { age: 25 };
Object.seal(person);
person.age = 30;    // Allowed
delete person.age; // Not allowed
console.log(person.age); // 30
```

---

## 3. Getters & Setters

- Define **computed properties** or intercept property access/modification.

Example:

```js
const user = {
  firstName: "Alice",
  lastName: "Johnson",
  get fullName() {
    return this.firstName + " " + this.lastName;
  },
  set fullName(name) {
    const [first, last] = name.split(" ");
    this.firstName = first;
    this.lastName = last;
  }
};

console.log(user.fullName); // Alice Johnson
user.fullName = "Bob Smith";
console.log(user.firstName); // Bob
```

---

## 4. Symbols & Iterators

### Symbols
- Unique, immutable identifiers used as object keys.
- Prevent property name collisions.

Example:

```js
const id = Symbol("id");
const user = {
  name: "Alice",
  [id]: 12345
};
console.log(user[id]); // 12345
```

### Iterators
- Objects that implement the ```Symbol.iterator``` method are **iterable** (e.g., arrays, strings).
- Can be looped with ```for...of```.

Example:

```js
const customIterable = {
  data: [1, 2, 3],
  [Symbol.iterator]() {
    let i = 0;
    return {
      next: () => ({
        value: this.data[i++],
        done: i > this.data.length
      })
    };
  }
};

for (const val of customIterable) {
  console.log(val); // 1, 2, 3
}
```

---

## Summary Table

| Feature                | Purpose                                         | Example                                |
|------------------------|-------------------------------------------------|----------------------------------------|
| writable               | Controls if property can be modified             | Object.defineProperty(..., {writable:false}) |
| configurable           | Controls if property can be deleted/redefined    | { configurable: false }                |
| enumerable             | Controls if property shows in loops              | { enumerable: false }                  |
| Object.freeze          | Makes object fully immutable                     | Object.freeze(obj)                     |
| Object.seal            | Prevents add/remove, allows modify existing      | Object.seal(obj)                       |
| Getters/Setters        | Custom access/modification logic                 | get fullName() { ... }                 |
| Symbols                | Unique property keys                            | const id = Symbol("id")                |
| Iterators              | Enable custom iteration behavior                 | ```[Symbol.iterator]() { ... }  ```          |
