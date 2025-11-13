# Module 1 — JavaScript Foundations

 Table of Contents

1. [What is JavaScript & How Browsers Execute It](#what-is-javascript--how-browsers-execute-it)
2. [Setting Up the Environment (VS Code + Node.js + Browser Console)](#setting-up-the-environment-vs-code--nodejs--browser-console)
3. [Variables: `var`, `let`, `const`](#variables-var-let-const)
4. [Data Types](#data-types)
5. [Operators](#operators)
6. [Type Conversion & Coercion](#type-conversion--coercion)
7. [Conditional Statements (`if`, `else`, `switch`)](#conditional-statements-if-else-switch)
8. [Loops (`for`, `while`, `do...while`, `for...of`, `for...in`)](#loops-for-while-dowhile-forof-forin)
9. [Functions (declarations, expressions, arrow functions)](#functions-declarations-expressions-arrow-functions)
10. [Scope & Hoisting](#scope--hoisting)
11. [Intro to `this` Keyword](#intro-to-this-keyword)
12. [Practice Exercises](#practice-exercises)

---

 What is JavaScript & How Browsers Execute It

Concept (instructor voice):
JavaScript is the language of the web — it adds behavior to HTML/CSS. Browsers include a JavaScript engine (V8 in Chrome, SpiderMonkey in Firefox, JavaScriptCore in Safari) that parses and executes JS. Execution is single-threaded with concurrency handled by the event loop.

Example: synchronous vs asynchronous

```javascript
// save as demo.js and run in browser console or Node
console.log("Start");

setTimeout(() => {
  console.log("From setTimeout (async)");
}, 10);

console.log("End");

// Expected order:
// Start
// End
// From setTimeout (async)
```

Pitfall: Students often expect asynchronous callbacks to execute immediately. Remember: async callbacks run later via the event loop.

Mini summary: JS runs in an engine; it is mostly single-threaded; asynchronous work uses event loop.

---

 Setting Up the Environment (VS Code + Node.js + Browser Console

Concept: You need a code editor to write JS, Node.js to run JS outside the browser, and browser devtools to quickly experiment.

Quick steps:

* Install VS Code ([https://code.visualstudio.com](https://code.visualstudio.com)).
* Install Node.js (LTS) ([https://nodejs.org](https://nodejs.org)).
* Open browser devtools: Chrome → `Ctrl+Shift+J` / `Cmd+Option+J`.

Example (Node):

Create `index.js`:

```javascript
// index.js
console.log("Hello from Node.js!");
```

Run from terminal:

```bash
node index.js
# => Hello from Node.js!
```

Example (Browser console):

Open console and type:

```javascript
console.log("Hello from Browser Console!");
```

Mini summary: Use VS Code for projects, Node for running scripts, browser console for quick testing.

---

 Variables: `var`, `let`, `const`

Concept: `var` is function-scoped (old), `let` and `const` are block-scoped (ES6). Use `const` for values that shouldn't change, `let` for reassignable variables.

Examples:

```javascript
// var example (function-scoped)
function varTest() {
  if (true) {
    var x = 1;
  }
  console.log(x); // 1 (x is visible here)
}

// let/const (block-scoped)
function letConstTest() {
  if (true) {
    let y = 2;
    const z = 3;
    // y = 5; // OK
    // z = 4; // Error: Assignment to constant variable.
  }
  // console.log(y); // ReferenceError
  // console.log(z); // ReferenceError
}
```

Pitfalls:

* `var` can lead to accidental globals and unexpected behavior due to hoisting.
* `const` prevents reassignment but not mutation for objects/arrays.

```javascript
const arr = [1, 2];
arr.push(3); // allowed
// arr = [4]; // not allowed
```

Mini summary: Prefer `const`, use `let` when you need to reassign; avoid `var`.

---

 Data Types

Concept: Primitive vs reference types. Primitives: `string`, `number`, `boolean`, `null`, `undefined`, `symbol`, `bigint`. Reference: `object` (including arrays, functions, objects).

Examples:

```javascript
// primitives
let s = "hello";       // string
let n = 42;            // number
let b = true;          // boolean
let u = undefined;     // undefined
let nl = null;         // null

// object / array
let obj = { name: "A" };
let arr = [1, 2, 3];
let fn = function () { return "I am a function"; };

// typeof
console.log(typeof s, typeof n, typeof b, typeof u, typeof nl, typeof obj, typeof arr, typeof fn);
// typeof null === "object" (historic JS quirk)
```

Pitfall: `typeof null` is `"object"` — a JS historical bug. Use explicit null checks when needed.

Mini summary: Know primitives vs reference types; objects and arrays are reference types and copied by reference.

---

 Operators

Concept: Operators let you compute values. Categories: arithmetic, comparison, logical, assignment, unary, ternary.

Examples:

```javascript
// arithmetic
console.log(1 + 2, 5 - 3, 4 * 2, 10 / 2, 7 % 3, 2  3);

// comparison
console.log(2 == "2");   // true  (loose equality)
console.log(2 === "2");  // false (strict equality)

// logical
console.log(true && false, true || false, !true);

// assignment
let a = 1;
a += 2; // a = 3

// ternary
const max = a > 10 ? "big" : "small";
```

Pitfalls:

* Prefer `===` over `==` to avoid coercion surprises.
* Know operator precedence for complex expressions.

Mini summary: Use strict equality (`===`); be mindful of coercion with `==`.

---

 Type Conversion & Coercion

Concept: Conversion (explicit) vs coercion (implicit). JS often coerces types in expressions.

Examples:

```javascript
// explicit conversion
Number("123"); // 123
String(123);   // "123"
Boolean(0);    // false

// coercion examples
console.log("5" - 2); // 3  (string coerced to number)
console.log("5" + 2); // "52" (2 coerced to string; + concatenates)
console.log([] + []); // "" (weird but true)
console.log([] + {}); // "[object Object]"
console.log({} + []); // 0 or "[object Object]" depending on context
```

Pitfall: `+` is concatenation when any operand is a string. Other arithmetic operators coerce to numbers.

Mini summary: Be explicit when converting types to avoid unexpected coercion.

---

 Conditional Statements (`if`, `else`, `switch`)

Concept: Branch program flow. Use `if/else` for most logic; `switch` is helpful for discrete multi-way branching.

Examples:

```javascript
// if / else
const score = 85;
if (score >= 90) {
  console.log("A");
} else if (score >= 75) {
  console.log("B");
} else {
  console.log("C");
}

// switch
const day = 2;
switch (day) {
  case 0:
    console.log("Sunday");
    break;
  case 1:
    console.log("Monday");
    break;
  default:
    console.log("Other day");
}
```

Pitfalls:

* Remember to use `break` in `switch` to avoid fall-through (unless intentional).
* Avoid deeply nested `if` blocks — consider extracting logic to functions.

Mini summary: `if/else` is flexible; `switch` is clean for many discrete choices.

---

 Loops (`for`, `while`, `do...while`, `for...of`, `for...in`)

Concept: Iterate over data. Use `for...of` for arrays (values), `for...in` for object keys (not recommended for arrays). Prefer modern iteration methods.

Examples:

```javascript
// for
for (let i = 0; i < 5; i++) {
  console.log(i);
}

// while
let i = 0;
while (i < 3) {
  console.log(i);
  i++;
}

// do...while
let j = 0;
do {
  console.log(j);
  j++;
} while (j < 2);

// for...of (array values)
const arr = ["a", "b", "c"];
for (const val of arr) {
  console.log(val);
}

// for...in (object keys)
const obj = { x: 1, y: 2 };
for (const key in obj) {
  console.log(key, obj[key]);
}
```

Pitfalls:

* Don’t use `for...in` with arrays — it iterates keys and may include inherited properties.
* Beware infinite loops with `while`/`for`.

Mini summary: Use `for...of` for arrays; `for...in` for enumerating object keys.

---

 Functions: Declarations, Expressions, Arrow Functions

Concept: Functions are first-class citizens. Function declaration hoists, function expressions do not. Arrow functions have lexical `this` and are concise.

Examples:

```javascript
// declaration (hoisted)
function greet(name) {
  return `Hello, ${name}`;
}

// expression (not hoisted)
const add = function (a, b) {
  return a + b;
};

// arrow function (lexical this)
const multiply = (a, b) => a * b;

// usage
console.log(greet("Student")); // Hello, Student
console.log(add(2, 3));       // 5
console.log(multiply(3, 4));  // 12
```

Pitfalls:

* Arrow functions don’t have their own `this` or `arguments`.
* Don’t use arrow functions as constructors (they can’t be used with `new`).

Mini summary: Use function declarations for named functions, expressions for flexible assignment, and arrow functions for concise callbacks and lexical `this`.

---

 Scope & Hoisting

Concept: Scope determines variable visibility. Hoisting moves declarations to the top of their scope — but initializations are not hoisted the same way.

Examples:

```javascript
// hoisting with var
console.log(a); // undefined (declaration hoisted, init not)
var a = 10;

// hoisting with let/const
// console.log(b); // ReferenceError: Cannot access 'b' before initialization
let b = 20;

// scope
function outer() {
  const outerVar = "outer";
  function inner() {
    console.log(outerVar); // can access outerVar due to lexical scope
  }
  inner();
}
outer();
```

Pitfalls:

* `var` is hoisted and can produce `undefined` instead of an error.
* Temporal Dead Zone (TDZ) for `let`/`const`: they cannot be accessed before initialization.

Mini summary: Prefer block-scoped `let`/`const`; understand hoisting to avoid surprising `undefined` values.

---

 Intro to `this` Keyword

Concept: `this` refers to execution context. In object methods it points to the object; in global context it’s `window` (or `undefined` in strict mode); arrow functions capture `this` lexically.

Examples:

```javascript
// method invocation
const person = {
  name: "Riya",
  sayHi() {
    console.log("Hi, I am", this.name);
  },
};
person.sayHi(); // Hi, I am Riya

// function invocation (non-strict)
function showThis() {
  console.log(this); // global object (window in browser) or undefined in strict mode
}
showThis();

// arrow function lexical this
const obj = {
  name: "Aman",
  arrow: () => {
    console.log(this); // not obj; inherits from outer scope
  },
};
obj.arrow();
```

Pitfalls:

* Arrow functions do not create their own `this`. Don’t use arrow functions as object methods if you need `this` to refer to the object.
* `this` in callbacks can be unexpected; use `.bind()` or arrow functions intentionally.

Mini summary: `this` depends on how a function is called. Arrow functions use surrounding `this` (lexical).

---

 Practice Exercises

Try these problems to solidify Module 1 concepts. Instructor notes included.

1. Hello Function
   Create an `index.js` with a function `greet(name)` that uses template literals to print `Hello, <name>!`.

2. Variable Behavior
   Write code that demonstrates the difference between `var` and `let` in block scope. Include comments explaining the output.

3. Type Coercion Quiz
   Predict the output for:

   ```javascript
   console.log("5" + 3);
   console.log("5" - 3);
   console.log(true + 2);
   console.log([] + []);
   ```

   Then run the code and explain why the result is what it is.

4. Sum Array
   Use a `for...of` loop to sum numbers in an array: `[4, 5, 6, 7]`.

5. Object Iteration
   Given:

   ```javascript
   const user = { id: 1, name: "Zara", active: true };
   ```

   Print both keys and values using `for...in`.

6. Arrow Function & `this`
   Create an object with a method using a normal function and another method using an arrow function. Log `this` inside both and explain the difference.

7. Hoisting Exercise
   Show an example where `var` produces `undefined` due to hoisting and where `let` throws a `ReferenceError` if used before declaration.

---

 Final Notes (Instructor Tips)

* Encourage students to copy-paste examples into Node or browser console to tinker. Active experimentation is the fastest way to learn JavaScript.
* Emphasize `const` by default, `let` when reassigning, avoid `var`.
* Teach debugging with `console.log`, browser breakpoints, and VS Code debugging.
* Keep the README as the living lecture note — update with new examples or clarifications as students ask questions.

---

If you want, I’ll now:

* Provide each section as an individual `SECTION_X.md` file, or
* Convert this README into a GitHub-flavored README with collapsible details and badges, or
* Generate separate slide-ready snippets for teaching.

Which one would you like next?
