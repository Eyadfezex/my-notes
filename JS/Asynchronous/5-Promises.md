# Promises

In JavaScript, a Promise is an object that represents the eventual completion (or failure) of an asynchronous operation. It acts as a placeholder for the result of an action that takes some time to finish, such as fetching data from a server or reading a file from disk.

**Key Concepts:**

- **Asynchronous Operations:** These are actions that take some time to complete, often involving interacting with external resources like servers or files. JavaScript doesn't wait for them to finish before continuing execution.
- **Promise States:** A Promise can be in one of three states:
  - **Pending:** The initial state, signifying that the operation hasn't finished yet.
  - **Fulfilled:** The operation completed successfully, with a resulting value.
  - **Rejected:** The operation encountered an error, with a reason (error object) explaining the failure.

```js
function fetchData(url) {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open("GET", url);
    xhr.onload = () => {
      if (xhr.status === 200) {
        resolve(xhr.responseText); // Fulfill with response data
      } else {
        reject(new Error(`Failed to fetch data: ${xhr.statusText}`)); // Reject with error reason
      }
    };
    xhr.onerror = () => reject(new Error("Network error")); // Reject on network error
    xhr.send();
  });
}
```

---

## async / await

- `async` keyword: When you declare a function with `async`, it becomes an asynchronous function. This function always returns a promise, even if you don't explicitly use the `Promise` constructor.

- `await` keyword: You can only use `await` inside an async function. It pauses the execution of the `async` function at that point until the awaited promise settles (resolves or rejects). Once the promise settles, the `await` keyword unwraps the resolved value and assigns it to a variable, or throws the rejection error if the promise is rejected.

```js
// A function that simulates an asynchronous operation, for example, fetching data from an API
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("Data fetched successfully!");
    }, 2000); // Simulating a delay of 2 seconds
  });
}

// An async function that makes use of await to wait for the result of the asynchronous operation
async function getData() {
  console.log("Fetching data...");
  try {
    const result = await fetchData(); // Wait until fetchData() completes
    console.log(result); // Print the fetched data
  } catch (error) {
    console.error("Error fetching data:", error);
  }
}

// Call the async function
getData();
```
