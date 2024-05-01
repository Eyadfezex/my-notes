# Strict mode

Strict mode in JavaScript is a way to write more secure and maintainable code. It eliminates some common errors and enforces stricter coding practices.

- **Eliminates undeclared variables:** In strict mode, trying to use a variable that hasn't been declared will throw a ReferenceError. This helps to prevent errors caused by typos or accidental use of undefined variables.
- **Prevents accidental modification of global variables:** By default, variables declared with var in strict mode are not added to the global scope. This helps to avoid accidentally modifying global variables and potential naming conflicts.
- **Restricts the use of with statement:** The with statement can be a source of confusion and errors. In strict mode, the use of with is discouraged.
- **Throws errors for some problematic practices:** Strict mode throws errors for some practices that can lead to errors, such as deleting a variable or setting a property on a non-writable object.

```js
"use strict";

// Your code here will be in strict mode
```
