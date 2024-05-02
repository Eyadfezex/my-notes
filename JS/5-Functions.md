# Functions

Functions exist so we can reuse code. They are blocks of code that execute whenever they are invoked.

```js
// Function to compute the product of p1 and p2
function myFunction(p1, p2) {
  return p1 * p2;
}
```

---

## Arrow Functions

Arrow functions were introduced in ES6.

```js
const hello = () => {
  return "Hello World!";
};
```

---

## IIFE (Immediately Invoked Function Expression)

Immediately-Invoked Function Expression is a function that is executed immediately after it is created.

```js
(function () {
  // …
})();

(() => {
  // …
})();

(async () => {
  // …
})();
```

---

## Arguments object

The `arguments` object is a local variable available within all non-arrow functions. You can refer to a function's `arguments` inside that function by using its `arguments` object. It has entries for each argument the function was called with, with the first entry's index at `0`.

```js
function func1(a, b, c) {
  console.log(arguments[0]);
  // Expected output: 1

  console.log(arguments[1]);
  // Expected output: 2

  console.log(arguments[2]);
  // Expected output: 3
}

func1(1, 2, 3);
```

---

## Call Stack

The call stack in JavaScript is like a to-do list for function calls. It follows **LIFO (Last-In-First-Out)** order. Each function call creates a frame on the stack, storing local variables, arguments, and the return address. This ensures functions run in order and keeps track of their context. Understanding the call stack is essential for complex JavaScript programs.

---

## Built in functions

A JavaScript method is a property containing a function definition. In other words, when the data stored on an object is a function we call that a method. [source](https://dev.to/elpepebenitez/built-in-methods-in-javascript-4bll)

---

## Recursion and stack

Recursion in JavaScript refers to a programming technique where a function calls itself within its own body. This creates a loop-like behavior where the function keeps executing itself with modified parameters until a certain condition is met.

```js
function factorial(n) {
  if (n === 0) {
    // Base case: factorial of 0 is 1
    return 1;
  } else {
    return n * factorial(n - 1); // Recursive step: n! = n * (n-1)!
  }
}

console.log(factorial(5)); // Output: 120
```

---

## Lexical scoping

Lexical scope is a fundamental concept in programming that determines where you can access variables and functions within your code. It's based on where things are defined in your program, rather than where they are called from.

```js
let globalVar = "This is global";

function outerFunction() {
  let outerVar = "This is outer";

  function innerFunction() {
    let innerVar = "This is inner";
    console.log(globalVar); // Accessing global variable
    console.log(outerVar); // Accessing outer variable
    console.log(innerVar); // Accessing inner variable
  }

  innerFunction();
}

outerFunction();
```

---

## Closures

A function along with its lexical environment is collectively called a closure.

```js
function createGreeter(name) {
  // Local variable within the outer function
  const greeting = "Hi";

  function sayHi() {
    console.log(greeting + ", " + name + "!");
  }

  // Return the inner function
  return sayHi;
}

// Call the outer function and store the returned function
const greetJohn = createGreeter("John");

// Call the inner function (greetJohn)
greetJohn(); // Output: Hi, John!
```
