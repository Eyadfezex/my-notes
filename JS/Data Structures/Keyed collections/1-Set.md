# Set

A `Set` is a special type collection – **“set of values”** (without keys), where each value may occur only once.

**Functionality:**

Stores a collection of unique values. No duplicates are allowed within a set.
Elements can be of any data type: numbers, strings, objects, etc.
Maintains insertion order. Elements are remembered in the order they were added (although iteration might not necessarily follow this order).

**Common Methods:**

- `add(value)`: Adds a new element to the set.
- `has(value)`: Returns `true` if the set contains the value, otherwise `false`.
- `size`: Returns the number of elements in the set.
- `delete(value)`: Removes a specific element from the set.
- `clear()`: Removes all elements from the set.

**Common Use Cases:**

Removing duplicate elements from an array.
Checking if a value exists in a collection.
Performing set operations like union, intersection, and difference (requires additional libraries).

```js
// ["sumit","amit","anil","anish"]
let set1 = new Set(["sumit", "sumit", "amit", "anil", "anish"]);

// it contains 'f', 'o', 'd'
let set2 = new Set("fooooooood");

// it contains [10, 20, 30, 40]
let set3 = new Set([10, 20, 30, 30, 40, 40]);

// it is an empty set
let set4 = new Set();
```
