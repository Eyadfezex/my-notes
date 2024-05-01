# Control Flow

In JavaScript, the `Control flow` is a way of how your computer runs code from top to bottom.

## Conditional statements

When you write code, you often want to perform different actions for different decisions. You can use conditional statements in your code to do this. In JavaScript, we have three conditional statements: `if`, `if...else`, and `switch`.

- `if`: The `if(...)` statement evaluates a condition in parentheses and, if the result is `true`, executes a block of code.
- `else`: Use the `else` statement to specify a block of code to be executed if the condition is `false`.
- `else if` : Use the `else if` statement to specify a new condition if the first condition is `false`.

```js
let year = prompt(
  "In which year was the ECMAScript-2015 specification published?",
  ""
);

if (year < 2015) {
  alert("Too early...");
} else if (year > 2015) {
  alert("Too late");
} else {
  alert("Exactly!");
}
```

- `switch`: Use the switch statement to select one of many code blocks to be executed.

```js
switch (new Date().getDay()) {
  case 0:
    day = "Sunday";
    break;
  case 1:
    day = "Monday";
    break;
  case 2:
    day = "Tuesday";
    break;
  case 3:
    day = "Wednesday";
    break;
  case 4:
    day = "Thursday";
    break;
  case 5:
    day = "Friday";
    break;
  case 6:
    day = "Saturday";
}
```

---

## Exception Handling

In JavaScript, all exceptions are simply objects. While the majority of exceptions are implementations of the global Error class, any old object can be thrown. With this in mind, there are two ways to throw an exception: directly via an Error object, and through a custom object. (excerpt from Rollbar)

- `try`: The `try` statement defines a code block to run (to try).

- `catch`: The `catch` statement defines a code block to handle any error.

- `finally`: The `finally` statement defines a code block to run regardless of the result.

- `throw`: The `throw` statement defines a custom error.

```js
function getRectArea(width, height) {
  if (isNaN(width) || isNaN(height)) {
    throw new Error("Parameter is not a number!");
  }
}

try {
  getRectArea(3, "A");
} catch (e) {
  console.error(e);
  // Expected output: Error: Parameter is not a number!
}
```
