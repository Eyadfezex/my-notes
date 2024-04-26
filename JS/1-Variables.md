# Variables

**`var`**

The `var` statement declares function-scoped or globally-scoped variables, optionally initializing each to a value.

```js
var x = 1;

if (x === 1) {
  var x = 2;

  console.log(x);
  // Expected output: 2
}

console.log(x);
// Expected output: 2
```

---

**`let`**

The `let` declaration declares re-assignable, block-scoped local variables, optionally initializing each to a value.

```js
let x = 1;

if (x === 1) {
  let x = 2;

  console.log(x);
  // Expected output: 2
}

console.log(x);
// Expected output: 1
```

---

**`const`**

The const declaration declares block-scoped local variables. The value of a constant can't be changed through reassignment using the assignment operator, but if a constant is an object, its properties can be added, updated, or removed.

```js
const number = 42;

try {
  number = 99;
} catch (err) {
  console.log(err);
  // Expected output: TypeError: invalid assignment to const 'number'
  // (Note: the exact output may be browser-dependent)
}

console.log(number);
// Expected output: 42
```

---

## Variables Scopes

Scope determines the accessibility (visibility) of variables.

- **Block Scope:** Variables declared inside a `{ }` block cannot be accessed from outside the block.

```js
{
  let x = 2;
}
// x can NOT be used here
```

- **Local Scope:** Variables declared within a JavaScript function, are **LOCAL** to the function.

```js
// code here can NOT use carName

function myFunction() {
  let carName = "Volvo";
  // code here CAN use carName
}

// code here can NOT use carName
```

- **Function Scope:** Variables defined inside a function are not accessible (visible) from outside the function.

```js
function myFunction() {
  var carName = "Volvo"; // Function Scope
}
```

---

## Hoisting

JavaScript Hoisting refers to the process whereby the interpreter appears to move the declaration of functions, variables, classes, or imports to the top of their scope, prior to execution of the code.

- In JavaScript, only `function` declarations (using function) are hoisted. This means you can call them before they're written in your code. However, this can be confusing and lead to errors.

- All variable declarations (using `var`, `let`, or `const`) are hoisted to the top of their scope during the hoisting phase.

- However, only `var` declarations are initialized with undefined during hoisting. `let` and `const` remain uninitialized until their definition is reached in the code.
