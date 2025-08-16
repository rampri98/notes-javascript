
# JavaScript: Objects & Arrays

## 1. Object Basics

- **Object Literal**: Easiest way to create an object in JavaScript.
  ```js
  const person = {
    name: "Alice",
    age: 25,
    isStudent: true
  };
  ```

- **Properties**:
  - Key-value pairs inside an object.
  - Keys are strings (implicitly), values can be any type (string, number, array, function, etc.).

## 2. Accessing & Modifying Properties

- **Dot notation**:
  ```js
  console.log(person.name); // "Alice"
  person.age = 26;          // modifies value
  ```

- **Bracket notation** (useful for dynamic keys or keys with spaces):
  ```js
  console.log(person["isStudent"]); // true
  person["age"] = 27;
  ```

- **Adding new properties**:
  ```js
  person.country = "India";
  ```

- **Deleting properties**:
  ```js
  delete person.age;
  ```

## 3. Object Utility Methods

- `Object.keys(obj)` → returns array of property names (keys).
  ```js
  Object.keys(person); // ["name", "isStudent", "country"]
  ```
- `Object.values(obj)` → returns array of values.
  ```js
  Object.values(person); // ["Alice", true, "India"]
  ```
- `Object.entries(obj)` → returns array of [key, value] pairs.
  ```js
  Object.entries(person); 
  // [["name", "Alice"], ["isStudent", true], ["country", "India"]]
  ```

## 4. Arrays Basics

- **Array creation**:
  ```js
  const numbers = [1, 2, 3, 4, 5];
  ```
- Arrays are ordered, zero-indexed collections.

## 5. Array Iteration Methods

- **forEach** → Executes a function for each element (no return value).
  ```js
  numbers.forEach(num => console.log(num));
  ```

- **map** → Returns a new array after applying a function.
  ```js
  const doubled = numbers.map(num => num * 2);
  ```

- **filter** → Returns new array with elements that pass a condition.
  ```js
  const evens = numbers.filter(num => num % 2 === 0);
  ```

- **reduce** → Reduces array to a single value (sum, product, etc.).
  ```js
  const sum = numbers.reduce((acc, num) => acc + num, 0);
  ```

- **find** → Returns the first element that matches condition.
  ```js
  const firstEven = numbers.find(num => num % 2 === 0);
  ```

- **some** → Returns true if at least one element passes condition.
  ```js
  const hasEven = numbers.some(num => num % 2 === 0);
  ```

- **every** → Returns true if all elements pass condition.
  ```js
  const allPositive = numbers.every(num => num > 0);
  ```

## 6. Spread Operator (`...`)

- **Copy arrays/objects**:
  ```js
  const numsCopy = [...numbers];
  const personCopy = { ...person };
  ```

- **Merge arrays**:
  ```js
  const merged = [...numbers, 6, 7];
  ```

- **Merge objects**:
  ```js
  const mergedObj = { ...person, hobby: "Reading" };
  ```
- **Rest** → Collects remaining elements into an array:
  ```js
  const [firstNum, ...restNums] = [1, 2, 3, 4];
  function sum(...nums) {
    return nums.reduce((a, b) => a + b);
  }
  ```

## 7. Destructuring

- **Array destructuring**:
  ```js
  const [first, second] = numbers; // first=1, second=2
  ```

- **Object destructuring**:
  ```js
  const { name, country } = person;
  ```

- **Renaming variables**:
  ```js
  const { name: personName } = person;
  ```

- **Default values**:
  ```js
  const { age = 18 } = person;
  ```
