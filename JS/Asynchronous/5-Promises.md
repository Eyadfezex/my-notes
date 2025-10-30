# Promises

In JavaScript, a **Promise** is an object that represents the eventual completion (or failure) of an asynchronous operation. It acts as a placeholder for the result of an action that takes some time to finish, such as fetching data from a server or reading a file from disk.

---

## Key Concepts

1. **Asynchronous Operations**:  
   Actions that take time to complete, often involving external resources like servers or files. JavaScript doesn't wait for them to finish before continuing execution.

2. **Promise States**:  
   A Promise can be in one of three states:

   - **Pending**: The initial state, indicating the operation hasn't finished yet.
   - **Fulfilled**: The operation completed successfully, with a resulting value.
   - **Rejected**: The operation encountered an error, with a reason (error object) explaining the failure.

3. **Promise Methods**:
   - `.then()`: Attaches a callback for when the Promise is fulfilled.
   - `.catch()`: Attaches a callback for when the Promise is rejected.
   - `.finally()`: Attaches a callback that runs regardless of the Promise's outcome.

---

## Example: Creating and Using a Promise

```javascript
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

// Using the Promise
fetchData("https://api.example.com/data")
  .then((data) => console.log("Data received:", data))
  .catch((error) => console.error("Error:", error));
```

---

## Chaining Promises

Promises can be chained to handle multiple asynchronous operations sequentially.

```javascript
fetchData("https://api.example.com/data")
  .then((data) => {
    console.log("Data received:", data);
    return processData(data); // Return a new Promise
  })
  .then((processedData) => {
    console.log("Processed data:", processedData);
  })
  .catch((error) => console.error("Error:", error));
```

---

## Error Handling

Use `.catch()` to handle errors in a Promise chain.

```javascript
fetchData("https://api.example.com/data")
  .then((data) => {
    console.log("Data received:", data);
    return processData(data);
  })
  .catch((error) => {
    console.error("Error:", error);
  });
```

---

# async / await

The `async` and `await` keywords provide a cleaner and more readable way to work with Promises.

---

## Key Concepts

1. **`async` Functions**:

   - Declare a function with `async` to make it asynchronous.
   - It always returns a Promise, even if you don't explicitly use the `Promise` constructor.

2. **`await` Keyword**:
   - Can only be used inside an `async` function.
   - Pauses the execution of the `async` function until the awaited Promise settles (resolves or rejects).
   - Unwraps the resolved value or throws the rejection error.

---

## Example: Using `async` and `await`

```javascript
// Simulate an asynchronous operation
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("Data fetched successfully!");
    }, 2000); // Simulate a 2-second delay
  });
}

// Async function using await
async function getData() {
  console.log("Fetching data...");
  try {
    const result = await fetchData(); // Wait for the Promise to resolve
    console.log(result); // Print the fetched data
  } catch (error) {
    console.error("Error fetching data:", error);
  }
}

// Call the async function
getData();
```

---

## Error Handling with `async/await`

Use `try/catch` blocks to handle errors in `async` functions.

```javascript
async function getData() {
  console.log("Fetching data...");
  try {
    const result = await fetchData();
    console.log(result);
  } catch (error) {
    console.error("Error fetching data:", error);
  }
}
```

---

## Combining `async/await` with Promises

You can mix `async/await` with traditional Promise methods.

```javascript
async function fetchAndProcessData() {
  try {
    const data = await fetchData("https://api.example.com/data");
    const processedData = await processData(data);
    console.log("Processed data:", processedData);
  } catch (error) {
    console.error("Error:", error);
  }
}
```

---

## Benefits of `async/await`

1. **Readability**: Code looks more synchronous and is easier to understand.
2. **Error Handling**: Simplifies error handling with `try/catch`.
3. **Debugging**: Easier to debug compared to deeply nested `.then()` chains.

---

## Best Practices

1. **Always Handle Errors**: Use `.catch()` or `try/catch` to handle errors in Promises and `async/await`.
2. **Avoid Blocking**: Use `await` judiciously to avoid blocking the event loop.
3. **Use `Promise.all` for Parallel Operations**: Run multiple asynchronous operations in parallel.

---

## Example: `Promise.all`

```javascript
async function fetchMultipleData() {
  try {
    const [data1, data2] = await Promise.all([
      fetchData("https://api.example.com/data1"),
      fetchData("https://api.example.com/data2"),
    ]);
    console.log("Data 1:", data1);
    console.log("Data 2:", data2);
  } catch (error) {
    console.error("Error fetching data:", error);
  }
}
```

---

## Resources

- [MDN Web Docs: Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
- [MDN Web Docs: async/await](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function)
- [JavaScript.info: Promises](https://javascript.info/promise-basics)
