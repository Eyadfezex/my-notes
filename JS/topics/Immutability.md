# Immutability

**Immutability** refers to the inability to change something after it has been created. If an object is immutable, it cannot be modified directly—any changes require creating a new object instead.

In JavaScript, **objects** and **arrays** are **mutable by default**, meaning their contents can be modified directly.

## Example: Mutable Updates

```javascript
// Modifying an object
const obj = { a: 1, b: 2 };
obj.b = 3; // Mutates the original object

// Modifying an array
const arr = ["a", "b"];
arr.push("c"); // Adds "c" to the array
arr[1] = "d"; // Changes the second element
```

Directly modifying data in this way can lead to unintended side effects, especially in large applications or when working with state in frameworks like React.

---

## Why is Immutability Important?

Immutability helps:

1. **Predictability**: Makes it easier to understand how data flows through your code.
2. **Debugging**: Reduces bugs caused by unexpected mutations.
3. **State Management**: Encourages cleaner state updates in libraries like Redux.

---

## Updating Data the Immutable Way

Instead of modifying objects or arrays directly, **create a copy, make changes to the copy, and use the new version**.

### Example: Updating Objects Immutably

Using the **spread operator**:

```javascript
const obj = { a: { c: 3 }, b: 2 };

// Create a shallow copy and update the property
const obj2 = { ...obj, b: 42 };

// Nested updates require spreading the inner objects
const obj3 = { ...obj, a: { ...obj.a, c: 42 } };

console.log(obj); // { a: { c: 3 }, b: 2 }
console.log(obj3); // { a: { c: 42 }, b: 2 }
```

---

### Example: Updating Arrays Immutably

Using **non-mutating methods** like `concat`, `slice`, or the spread operator:

```javascript
const arr = ["a", "b"];

// Using concat to add an element
const arr2 = arr.concat("c");

// Using slice to create a copy
const arr3 = arr.slice();
arr3.push("d");

// Using the spread operator
const arr4 = [...arr, "e"];

console.log(arr); // ["a", "b"]
console.log(arr2); // ["a", "b", "c"]
console.log(arr4); // ["a", "b", "e"]
```

---

### Key Notes

- **Shallow Copy**: Using the spread operator or methods like `slice` only copies the top-level properties of an object/array. For nested data structures, deeper levels will still reference the original object.
- **Deep Copy**: For fully independent copies, use libraries like Lodash or structured cloning with `structuredClone()`.

### Example: Deep Copy

```javascript
const obj = { a: { b: 2 }, c: 3 };

// Deep copy using structuredClone (browser-supported)
const objCopy = structuredClone(obj);

// Modifying the copy doesn't affect the original
objCopy.a.b = 42;

console.log(obj); // { a: { b: 2 }, c: 3 }
console.log(objCopy); // { a: { b: 42 }, c: 3 }
```
