# Async-logic

Asynchronous programming is a technique that enables your program to start a potentially long-running task and still be able to be responsive to other events while that task runs, rather than having to wait until that task has finished. Once that task has finished, your program is presented with the result.

**Common Techniques for Asynchronous JavaScript:**

- **Callbacks:** A function passed as an argument to be executed when an asynchronous operation finishes. This can lead to nested callbacks, making code hard to read.
- **Promises:** Objects representing the eventual completion (or failure) of an asynchronous operation. Promises provide a cleaner way to handle the results of asynchronous operations.
- **Async/Await:** Keywords introduced in ES2017 that provide a more synchronous-like way to write asynchronous code. They use promises behind the scenes but offer a simpler syntax.
