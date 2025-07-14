---
id: 15
date: 2025-07-14T00:00:00Z
title: JavaScript Cheatsheet
author: Jeremy Novak
summary: JavaScript programming language cheatsheet
slug: javascript-cheatsheet
tags:
  - javascript
published: true
---

# JavaScript Cheatsheet

---

## Setup & Environment

- Install Node.js (macOS)
```bash
brew install node
```

- Install Node.js (Linux)
```bash
# Ubuntu/Debian
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt-get install -y nodejs

# CentOS/RHEL
curl -fsSL https://rpm.nodesource.com/setup_lts.x | sudo bash -
sudo yum install -y nodejs
```

- Install Node.js (Windows)
1. Download from [nodejs.org](https://nodejs.org/)
2. Run installer and follow prompts
3. Or use package manager like Chocolatey

- Check versions
```bash
node --version
npm --version
```

- Initialize new project
```bash
npm init -y
```

---

## Running JavaScript

- Run JavaScript file with Node.js
```bash
node script.js
```

- Run JavaScript in browser
```html
<script src="script.js"></script>
<script>
    console.log("Hello, World!");
</script>
```

- Node.js REPL
```bash
node
```

---

## Variables and Data Types

- Variable declarations
```javascript
var oldWay = "avoid this";
let mutableVar = "can change";
const immutableVar = "cannot change";
```

- Numbers
```javascript
let integer = 42;
let float = 3.14;
let scientific = 1e6;
let infinity = Infinity;
let notANumber = NaN;
```

- Strings
```javascript
let single = 'Hello';
let double = "World";
let template = `Hello ${name}`;
let multiline = `This is a
multiline string`;
```

- Booleans
```javascript
let isTrue = true;
let isFalse = false;
```

- Arrays
```javascript
let numbers = [1, 2, 3, 4, 5];
let mixed = [1, "hello", true, null];
let empty = [];
```

- Objects
```javascript
let person = {
    name: "Alice",
    age: 30,
    greet: function() {
        return `Hello, I'm ${this.name}`;
    }
};
```

- Null and Undefined
```javascript
let nothing = null;
let notDefined = undefined;
```

---

## Functions

- Function declaration
```javascript
function greet(name) {
    return `Hello, ${name}!`;
}
```

- Function expression
```javascript
const greet = function(name) {
    return `Hello, ${name}!`;
};
```

- Arrow functions
```javascript
const greet = (name) => `Hello, ${name}!`;
const add = (a, b) => a + b;
const square = x => x * x;
```

- Default parameters
```javascript
function greet(name = "World") {
    return `Hello, ${name}!`;
}
```

- Rest parameters
```javascript
function sum(...numbers) {
    return numbers.reduce((total, num) => total + num, 0);
}
```

- Destructuring parameters
```javascript
function greet({name, age}) {
    return `Hello, ${name}! You are ${age} years old.`;
}
```

---

## Control Flow

- If/else statement
```javascript
if (x > 0) {
    console.log("Positive");
} else if (x < 0) {
    console.log("Negative");
} else {
    console.log("Zero");
}
```

- Ternary operator
```javascript
const message = x > 0 ? "Positive" : "Not positive";
```

- Switch statement
```javascript
switch (day) {
    case 1:
        console.log("Monday");
        break;
    case 2:
        console.log("Tuesday");
        break;
    default:
        console.log("Other day");
}
```

- For loop
```javascript
for (let i = 0; i < 10; i++) {
    console.log(i);
}
```

- For...of loop
```javascript
const array = [1, 2, 3, 4, 5];
for (const item of array) {
    console.log(item);
}
```

- For...in loop
```javascript
const obj = {a: 1, b: 2, c: 3};
for (const key in obj) {
    console.log(key, obj[key]);
}
```

- While loop
```javascript
let i = 0;
while (i < 10) {
    console.log(i);
    i++;
}
```

---

## Arrays

- Array methods
```javascript
const numbers = [1, 2, 3, 4, 5];

// Add/remove elements
numbers.push(6);           // Add to end
numbers.pop();             // Remove from end
numbers.unshift(0);        // Add to beginning
numbers.shift();           // Remove from beginning

// Transform arrays
const doubled = numbers.map(x => x * 2);
const evens = numbers.filter(x => x % 2 === 0);
const sum = numbers.reduce((acc, x) => acc + x, 0);

// Find elements
const found = numbers.find(x => x > 3);
const index = numbers.findIndex(x => x > 3);
const includes = numbers.includes(3);

// Sort and reverse
numbers.sort((a, b) => a - b);
numbers.reverse();

// Join and slice
const joined = numbers.join(", ");
const sliced = numbers.slice(1, 3);
```

- Array destructuring
```javascript
const [first, second, ...rest] = [1, 2, 3, 4, 5];
```

---

## Objects

- Object methods
```javascript
const person = {name: "Alice", age: 30};

// Get keys, values, entries
Object.keys(person);       // ["name", "age"]
Object.values(person);     // ["Alice", 30]
Object.entries(person);    // [["name", "Alice"], ["age", 30]]

// Assign and merge
Object.assign(person, {city: "New York"});
const merged = {...person, country: "USA"};

// Check properties
person.hasOwnProperty("name");  // true
"name" in person;               // true
```

- Object destructuring
```javascript
const {name, age} = person;
const {name: userName, age: userAge} = person;
```

- Object shorthand
```javascript
const name = "Alice";
const age = 30;
const person = {name, age};  // Same as {name: name, age: age}
```

---

## Classes

- Class declaration
```javascript
class Person {
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }
    
    greet() {
        return `Hello, I'm ${this.name}`;
    }
    
    static species() {
        return "Homo sapiens";
    }
}
```

- Class inheritance
```javascript
class Student extends Person {
    constructor(name, age, studentId) {
        super(name, age);
        this.studentId = studentId;
    }
    
    study() {
        return `${this.name} is studying`;
    }
}
```

- Getters and setters
```javascript
class Circle {
    constructor(radius) {
        this._radius = radius;
    }
    
    get radius() {
        return this._radius;
    }
    
    set radius(value) {
        if (value < 0) {
            throw new Error("Radius cannot be negative");
        }
        this._radius = value;
    }
    
    get area() {
        return Math.PI * this._radius ** 2;
    }
}
```

---

## Promises and Async/Await

- Creating promises
```javascript
const promise = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve("Success!");
    }, 1000);
});
```

- Using promises
```javascript
promise
    .then(result => console.log(result))
    .catch(error => console.error(error))
    .finally(() => console.log("Done"));
```

- Async/await
```javascript
async function fetchData() {
    try {
        const response = await fetch('https://api.example.com/data');
        const data = await response.json();
        return data;
    } catch (error) {
        console.error('Error:', error);
    }
}
```

- Promise utilities
```javascript
Promise.all([promise1, promise2, promise3])
    .then(results => console.log(results));

Promise.race([promise1, promise2, promise3])
    .then(result => console.log(result));

Promise.allSettled([promise1, promise2, promise3])
    .then(results => console.log(results));
```

---

## Error Handling

- Try/catch/finally
```javascript
try {
    const result = riskyOperation();
    console.log(result);
} catch (error) {
    console.error('Error:', error.message);
} finally {
    console.log('Cleanup');
}
```

- Throwing errors
```javascript
function divide(a, b) {
    if (b === 0) {
        throw new Error("Division by zero");
    }
    return a / b;
}
```

- Custom errors
```javascript
class ValidationError extends Error {
    constructor(message) {
        super(message);
        this.name = "ValidationError";
    }
}

throw new ValidationError("Invalid input");
```

---

## Modules (ES6)

- Export
```javascript
// utils.js
export function add(a, b) {
    return a + b;
}

export const PI = 3.14159;

export default function greet(name) {
    return `Hello, ${name}!`;
}
```

- Import
```javascript
// main.js
import greet, {add, PI} from './utils.js';
import * as utils from './utils.js';
```

- CommonJS (Node.js)
```javascript
// Export
module.exports = {
    add: (a, b) => a + b,
    PI: 3.14159
};

// Import
const {add, PI} = require('./utils');
```

---

## DOM Manipulation

- Selecting elements
```javascript
const element = document.getElementById('myId');
const elements = document.getElementsByClassName('myClass');
const element = document.querySelector('.myClass');
const elements = document.querySelectorAll('div');
```

- Modifying elements
```javascript
element.textContent = 'New text';
element.innerHTML = '<strong>Bold text</strong>';
element.setAttribute('class', 'newClass');
element.classList.add('active');
element.classList.remove('inactive');
element.classList.toggle('visible');
```

- Creating elements
```javascript
const newDiv = document.createElement('div');
newDiv.textContent = 'Hello';
document.body.appendChild(newDiv);
```

- Event handling
```javascript
button.addEventListener('click', function(event) {
    console.log('Button clicked!');
});

button.addEventListener('click', (event) => {
    event.preventDefault();
    console.log('Default prevented');
});
```

---

## Local Storage

- Store data
```javascript
localStorage.setItem('username', 'Alice');
localStorage.setItem('user', JSON.stringify({name: 'Alice', age: 30}));
```

- Retrieve data
```javascript
const username = localStorage.getItem('username');
const user = JSON.parse(localStorage.getItem('user'));
```

- Remove data
```javascript
localStorage.removeItem('username');
localStorage.clear(); // Remove all
```

---

## Fetch API

- GET request
```javascript
fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

- POST request
```javascript
fetch('https://api.example.com/data', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
    },
    body: JSON.stringify({name: 'Alice', age: 30})
})
.then(response => response.json())
.then(data => console.log(data));
```

- With async/await
```javascript
async function fetchData() {
    try {
        const response = await fetch('https://api.example.com/data');
        const data = await response.json();
        return data;
    } catch (error) {
        console.error('Error:', error);
    }
}
```

---

## Common Built-in Objects

- String methods
```javascript
const str = "Hello World";
str.length;                    // 11
str.toUpperCase();             // "HELLO WORLD"
str.toLowerCase();             // "hello world"
str.charAt(0);                 // "H"
str.indexOf("World");          // 6
str.slice(0, 5);              // "Hello"
str.split(" ");               // ["Hello", "World"]
str.replace("World", "JS");    // "Hello JS"
str.includes("World");         // true
str.startsWith("Hello");       // true
str.endsWith("World");         // true
```

- Math object
```javascript
Math.PI;                      // 3.141592653589793
Math.round(4.7);              // 5
Math.floor(4.7);              // 4
Math.ceil(4.3);               // 5
Math.max(1, 2, 3);            // 3
Math.min(1, 2, 3);            // 1
Math.random();                // 0-1
Math.sqrt(16);                // 4
Math.pow(2, 3);               // 8
```

- Date object
```javascript
const now = new Date();
const specific = new Date('2023-01-01');
now.getFullYear();            // 2023
now.getMonth();               // 0-11
now.getDate();                // 1-31
now.getHours();               // 0-23
now.toISOString();            // "2023-01-01T00:00:00.000Z"
now.toLocaleDateString();     // "1/1/2023"
```

---

## Regular Expressions

- Creating regex
```javascript
const regex = /pattern/flags;
const regex = new RegExp('pattern', 'flags');
```

- Common methods
```javascript
const str = "Hello World";
const regex = /world/i;

regex.test(str);              // true
str.match(regex);             // ["World"]
str.replace(regex, "JS");     // "Hello JS"
str.split(/\s+/);             // ["Hello", "World"]
```

- Common patterns
```javascript
const email = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
const phone = /^\d{3}-\d{3}-\d{4}$/;
const url = /^https?:\/\/.+/;
```

---

## Package Management (npm)

- Install package
```bash
npm install package-name
npm install -g package-name     # Global
npm install --save-dev package-name  # Dev dependency
```

- Common commands
```bash
npm init                        # Initialize project
npm install                     # Install dependencies
npm start                       # Run start script
npm test                        # Run tests
npm run build                   # Run build script
npm update                      # Update packages
npm outdated                    # Check outdated packages
```

- package.json scripts
```json
{
  "scripts": {
    "start": "node server.js",
    "test": "jest",
    "build": "webpack",
    "dev": "nodemon server.js"
  }
}
```

---

## Common Patterns

- Immediately Invoked Function Expression (IIFE)
```javascript
(function() {
    console.log("IIFE executed");
})();
```

- Module pattern
```javascript
const MyModule = (function() {
    let privateVar = 0;
    
    return {
        increment: function() {
            privateVar++;
        },
        getCount: function() {
            return privateVar;
        }
    };
})();
```

- Debouncing
```javascript
function debounce(func, delay) {
    let timeoutId;
    return function(...args) {
        clearTimeout(timeoutId);
        timeoutId = setTimeout(() => func.apply(this, args), delay);
    };
}
```

- Throttling
```javascript
function throttle(func, limit) {
    let inThrottle;
    return function(...args) {
        if (!inThrottle) {
            func.apply(this, args);
            inThrottle = true;
            setTimeout(() => inThrottle = false, limit);
        }
    };
}
```

---

## Testing

- Jest example
```javascript
// sum.js
function sum(a, b) {
    return a + b;
}
module.exports = sum;

// sum.test.js
const sum = require('./sum');

test('adds 1 + 2 to equal 3', () => {
    expect(sum(1, 2)).toBe(3);
});
```

- Basic assertions
```javascript
expect(value).toBe(expected);
expect(value).toEqual(expected);
expect(value).toBeNull();
expect(value).toBeUndefined();
expect(value).toBeTruthy();
expect(value).toBeFalsy();
expect(array).toContain(item);
```

---

## Useful Libraries

- Lodash — Utility library
```javascript
const _ = require('lodash');
_.uniq([1, 2, 2, 3]); // [1, 2, 3]
```

- Moment.js — Date manipulation
```javascript
const moment = require('moment');
moment().format('YYYY-MM-DD');
```

- Axios — HTTP client
```javascript
const axios = require('axios');
axios.get('https://api.example.com/data')
    .then(response => console.log(response.data));
```

---

## Resources

- [MDN Web Docs](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
- [JavaScript.info](https://javascript.info/)
- [Node.js Documentation](https://nodejs.org/en/docs/)
- [npm Registry](https://www.npmjs.com/)
- [ES6 Features](http://es6-features.org/)
