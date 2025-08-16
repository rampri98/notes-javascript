
# JavaScript: Error Handling

Error handling in JavaScript ensures that your code can gracefully respond to unexpected situations.

---

## 1. `try...catch...finally`

- **`try`** → Code that might throw an error.
- **`catch`** → Handles the error if it occurs.
- **`finally`** → Runs after try/catch, regardless of outcome.

Example:
```js
try {
  let result = riskyFunction();
  console.log(result);
} catch (error) {
  console.error("An error occurred:", error.message);
} finally {
  console.log("Cleanup actions go here.");
}
```

---

## 2. `throw`

- Manually throw an error when certain conditions occur.
- Can throw any type (string, number, object), but best practice is to throw `Error` objects.

Example:
```js
function divide(a, b) {
  if (b === 0) {
    throw new Error("Division by zero is not allowed");
  }
  return a / b;
}

try {
  divide(4, 0);
} catch (err) {
  console.error(err.name, err.message);
}
```

---

## 3. Custom Error Objects

- Create custom error classes for more specific error handling.
- Inherit from the built-in `Error` class.

Example:
```js
class ValidationError extends Error {
  constructor(message) {
    super(message);
    this.name = "ValidationError";
  }
}

function processInput(input) {
  if (!input) {
    throw new ValidationError("Input is required");
  }
  console.log("Processing:", input);
}

try {
  processInput("");
} catch (err) {
  if (err instanceof ValidationError) {
    console.error("Validation failed:", err.message);
  } else {
    console.error("Unexpected error:", err);
  }
}
```

---

**Summary Table:**

| Feature              | Purpose                                       |
|----------------------|-----------------------------------------------|
| try...catch...finally| Handle runtime errors gracefully              |
| throw                | Trigger custom errors manually                |
| Custom Error Objects | Create meaningful, specific error types       |
