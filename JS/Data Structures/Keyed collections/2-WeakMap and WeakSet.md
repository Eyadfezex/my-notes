# WeakMap and WeakSet

## WeakMap

A `WeakMap` is a collection of key-value pairs in JavaScript with special properties for keys and memory management. Here's the breakdown:

- **Keys:**

  - Can only be objects, not primitive values like numbers or strings.
  - Weak references are used for keys. This means when the object key is no longer referenced anywhere else in your code, it gets garbage collected.

- **Values:**

  - Can be any data type (strings, numbers, objects, etc.).

- **Memory Management:**

  - The key difference from a regular Map. When the object key is garbage collected, the corresponding value in the WeakMap is also removed automatically. This helps prevent memory leaks.

- **Limitations:**
  - Due to the dynamic nature of key removal during garbage collection, WeakMaps don't support methods to iterate over all keys or values (like `keys()`, `values()`, or `entries()` in a Map).

**Use Cases:**

- **Additional Data:** Store data associated with objects from external libraries or code. This data disappears when the object itself is garbage collected.
- **Caching:** Cache function results based on objects. When the object is no longer needed, the cached data disappears automatically.

```js
// Cache function to avoid redundant calculations
let cache = new WeakMap();

function process(obj) {
  if (!cache.has(obj)) {
    // Simulate some expensive calculation based on the object
    let result = `Calculation result for ${JSON.stringify(obj)}`;
    cache.set(obj, result);
    return result;
  }

  return cache.get(obj);
}

// Usage
let someObject = { name: "Alice" };

let result1 = process(someObject); // Cache miss, calculates the result
console.log(result1); // Output: Calculation result for {"name":"Alice"}

let result2 = process(someObject); // Cache hit, retrieves from cache
console.log(result2); // Output: Calculation result for {"name":"Alice"}

// Later, when the object is no longer needed
someObject = null;

// Cache automatically cleans up with the object
```

---

## WeakSet

- **Weak References:** Objects stay in the set as long as they're used elsewhere. Once alone, they're garbage collected, preventing memory leaks.
- **Limited Functionality:** Supports `add`, `has`, and `delete`, but no iteration or size checks due to dynamic membership.

**Use for:**

- Storing extra data for objects from other parts of your code. This data disappears when the object itself is no longer needed.
- Caching results based on objects. The cache entry is automatically removed when the object is gone.

```js
// Create a WeakSet to store DOM nodes (assuming they're objects)
const specialNodes = new WeakSet();

// Function to mark a DOM node as special
function markSpecial(node) {
  specialNodes.add(node);
}

// Create some DOM nodes (simulated objects)
const node1 = {};
const node2 = {};

// Mark node1 as special
markSpecial(node1);

// Check if node1 is special
console.log("node1 is special:", specialNodes.has(node1)); // true
console.log("node2 is special:", specialNodes.has(node2)); // false
```
