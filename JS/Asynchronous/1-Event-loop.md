# Event Loop in JavaScript

The event loop is a fundamental concept in JavaScript that enables non-blocking I/O operations, even though JavaScript is single-threaded. It achieves this by offloading operations to the operating system or browser APIs whenever possible.

---

## Key Components

### Call Stack

- Think of the call stack as a stack of plates, where each plate represents a function being executed.
- The event loop processes functions one at a time, in the order they were called.
- When a function is called, it is added to the stack. When it finishes executing, it is removed from the stack.

### Event Queue (Callback Queue)

- This is where asynchronous operations (like `setTimeout`, `fetch`, or DOM events) place their callbacks once they are completed.
- Examples of such operations include:
  - Timers (`setTimeout`, `setInterval`)
  - User interactions (clicks, key presses)
  - Web API responses (e.g., data from a network request)

### Event Loop

The event loop is a continuous process that performs the following steps:

1. **Check if the call stack is empty**.
2. If the call stack is empty, **pull the next callback from the event queue** and push it onto the call stack for execution.
3. If the call stack is not empty, continue executing the current function.

---

## How It Works in a Browser

When JavaScript code runs in a browser, the event loop orchestrates the execution of synchronous and asynchronous tasks. Here's a step-by-step breakdown:

1. **Synchronous Code Execution**:

   - The JavaScript engine starts by executing synchronous code line by line.
   - Each function call is added to the **call stack**, executed, and then removed once completed.

2. **Asynchronous Operations**:

   - When an asynchronous operation (like `setTimeout`, `fetch`, or a DOM event) is encountered, it is handed off to the browser's Web APIs.
   - These APIs handle the operation in the background, freeing up the main thread to continue executing other code.

3. **Callback Queue**:

   - Once the asynchronous operation completes (e.g., a timer expires or a network request finishes), its callback is placed in the **event queue**.

4. **Event Loop in Action**:
   - The event loop constantly monitors the **call stack** and the **event queue**.
   - When the call stack is empty, the event loop takes the first callback from the event queue and pushes it onto the call stack for execution.

---

## Example Scenario

Consider the following code:

```javascript
console.log("Start");

setTimeout(() => {
  console.log("Timeout callback");
}, 1000);

console.log("End");
```

### Execution Steps:

1. `console.log("Start")` is executed and removed from the call stack.
2. `setTimeout` is encountered and handed off to the browser's timer API. The timer starts, and the main thread moves on.
3. `console.log("End")` is executed and removed from the call stack.
4. After 1 second, the timer completes, and the callback (`console.log("Timeout callback")`) is placed in the event queue.
5. The event loop checks the call stack, finds it empty, and pushes the callback onto the call stack for execution.

---

## Non-Blocking Nature

- The event loop ensures that long-running operations (like network requests or file I/O in Node.js) don’t block the main thread.
- Instead, they are handled asynchronously, allowing the application to remain responsive.
