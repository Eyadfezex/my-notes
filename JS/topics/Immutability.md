# Immutability

**Mutable** means **changeable**. If something is **immutable**, it can never be changed.

In JavaScript, objects and arrays are mutable by default, meaning their contents can be changed directly. For example:

```javascript
const obj = { a: 1, b: 2 };
obj.b = 3;

const arr = ["a", "b"];
arr.push("c");
arr[1] = "d";
```

To update values immutably, you need to create copies of existing objects/arrays and then modify those copies. This can be done using spread operators or array methods that return new copies:

```javascript
const obj = { a: { c: 3 }, b: 2 };
const obj2 = { ...obj, a: { ...obj.a, c: 42 } };

const arr = ["a", "b"];
const arr2 = arr.concat("c");

const arr3 = arr.slice();
arr3.push("c");
```
