# Error Handling in Node.js

## Overview

Error handling is a critical aspect of Node.js applications, ensuring that the system can gracefully manage and respond to unexpected issues. Node.js provides built-in error classes, such as `SystemError` and `AssertionError`, to handle errors related to system operations and assertions.

---

## Types of Errors in Node.js

### 1. SystemError

- **Definition**: A `SystemError` is thrown when an error occurs within the Node.js runtime environment, typically due to system-level operations like file I/O, network requests, or process execution.
- **Common Causes**:
  - File not found (`ENOENT`).
  - Permission denied (`EACCES`).
  - Connection refused (`ECONNREFUSED`).
  - Out of memory (`ENOMEM`).
- **Properties**:
  - `code`: A string representing the error code (e.g., `ENOENT`, `EACCES`).
  - `errno`: A number representing the error number.
  - `syscall`: A string describing the system call that triggered the error.
  - `path` or `address`: Additional context about the error (e.g., file path or network address).

#### Code Example:

```javascript
const fs = require("fs");

try {
  // Attempt to read a non-existent file
  fs.readFileSync("/path/to/nonexistent/file.txt", "utf8");
} catch (err) {
  if (err.code === "ENOENT") {
    console.error("SystemError: File not found:", err.path);
  } else {
    console.error("SystemError:", err.message);
  }
}
```

---

### 2. AssertionError

- **Definition**: An `AssertionError` is thrown when an assertion fails. This error is commonly used in testing and debugging to ensure that certain conditions are met.
- **Properties**:
  - `message`: A description of the error.
  - `actual`: The actual value that caused the assertion to fail.
  - `expected`: The expected value that was not met.
  - `operator`: The operation that was performed (e.g., `==`, `===`).
  - `generatedMessage`: Indicates whether the message was auto-generated.

#### Code Example:

```javascript
const assert = require("assert");

try {
  // Assert that two values are equal
  assert.strictEqual(1, 2); // This will throw an AssertionError
} catch (err) {
  console.error("AssertionError:", err.message);
  console.error("Expected:", err.expected);
  console.error("Actual:", err.actual);
}
```

---

### 3. User-Specified Errors

- **Definition**: Errors triggered by invalid or unexpected user inputs.
- **Examples**:
  - Incorrect data format.
  - Missing required fields.
  - Out-of-range values.
- **Handling**:
  - Validate user inputs before processing.
  - Provide clear error messages to guide users.

#### Code Example:

```javascript
function validateUserInput(input) {
  if (!input || typeof input !== "string") {
    throw new Error("Invalid input: Input must be a non-empty string.");
  }
  if (input.length > 100) {
    throw new Error("Invalid input: Input must be less than 100 characters.");
  }
}

try {
  validateUserInput(""); // This will throw an error
} catch (err) {
  console.error("User-Specified Error:", err.message);
}
```

---

### 4. JavaScript Errors

- **Definition**: Errors specific to JavaScript, often arising from syntax issues, type mismatches, or runtime exceptions.
- **Examples**:
  - `SyntaxError`: Invalid JavaScript syntax.
  - `TypeError`: Incorrect data type used in an operation.
  - `ReferenceError`: Accessing an undefined variable.
- **Handling**:
  - Use try-catch blocks to handle runtime errors.
  - Leverage linters and static analysis tools to catch syntax errors early.

#### Code Example:

```javascript
try {
  const obj = undefined;
  console.log(obj.name); // This will throw a TypeError
} catch (err) {
  console.error("JavaScript Error:", err.message);
}
```

---

## Best Practices for Error Handling in Node.js

1. **Graceful Degradation**:

   - Ensure the application can continue functioning, even if some features fail.

2. **Logging**:

   - Log errors with sufficient context for debugging.
   - Use logging levels (e.g., info, warn, error) to categorize issues.

3. **User Feedback**:

   - Provide clear and actionable error messages to users.
   - Avoid exposing sensitive information in error messages.

4. **Testing**:

   - Write unit tests to cover error scenarios.
   - Use tools like static analyzers and linters to catch potential issues early.

5. **Retry Mechanisms**:
   - Implement retries for transient errors (e.g., network timeouts).

---

## References

- [Node.js SystemError Documentation](https://nodejs.org/api/errors.html#errors_class_systemerror)
- [Node.js AssertionError Documentation](https://nodejs.org/api/assert.html#new-assertassertionerroroptions)
- [MDN Web Docs on JavaScript Errors](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Error)
- Best Practices in Error Handling by various software development resources.
