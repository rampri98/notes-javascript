
# JavaScript: Prototypes & Inheritance

JavaScript uses **prototype-based inheritance**, meaning objects can inherit properties and methods from other objects via a **prototype chain**.

---

## 1. Prototype Chain

- Every JavaScript object has an internal link to another object called its **prototype**.
- The prototype itself may have its own prototype, forming a **prototype chain**.
- The chain ends with `Object.prototype`, whose prototype is `null`.

Example:
```js
const obj = {};
console.log(Object.getPrototypeOf(obj) === Object.prototype); // true
```

Property Lookup Process:
1. Look for the property on the object itself.
2. If not found, look at its prototype.
3. Continue up the chain until found or prototype is `null`.

---

## 2. `Object.create()` & `Object.setPrototypeOf()`

- **Object.create(proto)** → creates a new object with the specified prototype.
```js
const animal = { eats: true };
const dog = Object.create(animal);
console.log(dog.eats); // true (inherited)
```

- **Object.setPrototypeOf(obj, proto)** → sets the prototype of an existing object.
```js
const cat = {};
Object.setPrototypeOf(cat, animal);
console.log(cat.eats); // true
```

---

## 3. Constructor Functions & `prototype` Property

- A **constructor function** is used to create multiple similar objects.
```js
function Person(name) {
  this.name = name;
}
Person.prototype.sayHello = function() {
  console.log("Hello, I'm " + this.name);
};
const alice = new Person("Alice");
alice.sayHello(); // "Hello, I'm Alice"
```

- The `prototype` property of a constructor is the object that will be assigned as the prototype of instances created by `new`.
- `constructor` property:
```js
console.log(alice.constructor === Person); // true
```

---

## 4. Inheritance Patterns

### ES5 (Prototype Chaining with Constructor Functions)
```js
function Animal(type) {
  this.type = type;
}
Animal.prototype.eat = function() {
  console.log(this.type + " is eating");
};

function Dog(name) {
  Animal.call(this, "Dog"); // Call parent constructor
  this.name = name;
}
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;

Dog.prototype.bark = function() {
  console.log(this.name + " barks!");
};

const rex = new Dog("Rex");
rex.eat(); // "Dog is eating"
rex.bark(); // "Rex barks!"
```

### ES6 (Class Syntax)
```js
class Animal {
  constructor(type) {
    this.type = type;
  }
  eat() {
    console.log(this.type + " is eating");
  }
}

class Dog extends Animal {
  constructor(name) {
    super("Dog"); // Call parent constructor
    this.name = name;
  }
  bark() {
    console.log(this.name + " barks!");
  }
}

const rex = new Dog("Rex");
rex.eat(); // "Dog is eating"
rex.bark(); // "Rex barks!"
```

---

**Summary Table:**

| Feature                | ES5 Constructor Function           | ES6 Class Syntax            |
|------------------------|-------------------------------------|-----------------------------|
| Syntax                 | Verbose, manual prototype setup     | Cleaner, `class` keyword    |
| Inheritance            | `Object.create()` + constructor call| `extends` + `super()`       |
| `this` binding         | Manual call with `.call`/`.apply`   | Automatic in constructor    |
