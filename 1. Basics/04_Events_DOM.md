# JavaScript Events & DOM Basics – Interview Prep Notes

## 1. Selecting Elements
- Access elements in the DOM to manipulate them.

### a. getElementById
- Selects a single element by its id.  
```javascript
let heading = document.getElementById("myHeading");  
console.log(heading);
```
### b. getElementsByTagName
- Selects all elements with a specific tag name.
- Returns an HTMLCollection.
```javascript
let paragraphs = document.getElementsByTagName("p");
console.log(paragraphs);
console.log(paragraphs[0]); // First paragraph
```


### c. querySelectorAll
- Selects all elements matching a CSS selector.
- Returns a NodeList (static collection).
```javascript
let buttons = document.querySelectorAll(".btn");
buttons.forEach(btn => console.log(btn));
```

### d. closest
- Selects the closest ancestor that matches a selector.
```javascript
let child = document.querySelector(".child");
let parent = child.closest(".parent");
console.log(parent);
```

### e. parentElement / children / nextElementSibling / previousElementSibling
- Navigate the DOM tree relative to a known element.
```javascript
let item = document.querySelector(".item");
console.log(item.parentElement);        // Parent element
console.log(item.children);             // Child elements
console.log(item.nextElementSibling);   // Next sibling
console.log(item.previousElementSibling); // Previous sibling
```

## 2. Event Handling
- Attach actions to user interactions.

### a. Inline onclick
- Add events directly in HTML.  
```javascript
<button onclick="sayHello()">Click me</button>  
Function: function sayHello() { alert("Hello!"); }
```

### b. addEventListener
- Preferred method; can attach multiple events.  
```javascript
let button = document.querySelector(".btn");  
button.addEventListener("click", () => { alert("Button clicked!"); });
```

## 3. Event Object
- Automatically passed to event handlers; contains info about the event.  
```javascript
button.addEventListener("click", (e) => {  
- e.type gives the type of event, e.target gives the element clicked  
});
```

## 4. Basic DOM Manipulation
### a. innerHTML
- Get or set the HTML content of an element.  
```javascript
let div = document.querySelector("#myDiv");  
div.innerHTML = "<p>New content</p>";
```

### b. style
- Change CSS styles directly.  
```javascript
div.style.color = "red";  
div.style.backgroundColor = "yellow";
```

### c. classList
- Add, remove, or toggle classes.  
```javascript
div.classList.add("active");  
div.classList.remove("inactive");  
div.classList.toggle("highlight");
```
