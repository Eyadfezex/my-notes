# Arrays

**Arrays: Ordered Collections of Data**

- Used to store lists of items in a specific order.
- Elements are accessed using numerical indexes starting from 0.

**Creation:**

- `let fruits = ["Apple", "Orange", "Plum"];` (preferred)
- `let arr = new Array("item1", "item2", ...);` (less common)

**Accessing Elements:**

- `fruits[0]` - gets the first element ("Apple").
- `arr.at(-1)` - gets the last element (using the `at` method for negative indexes).

**Adding/Removing Elements:**

- **End:**
  - `fruits.push("Pear")` - adds "Pear" to the end.
  - `fruits.pop()` - removes the last element and returns it.
- **Beginning:**
  - `fruits.unshift("Pineapple")` - adds "Pineapple" to the beginning.
  - `fruits.shift()` - removes the first element and returns it.

**Looping:**

- `for (let i = 0; i < fruits.length; i++) { ... }` - traditional loop with index.
- `for (let fruit of fruits) { ... }` - modern loop for iterating over elements.

**Important Notes:**

- Arrays are objects internally, but optimized for ordered data.
- Don't use `==` for array comparison; iterate and compare elements.
- `length` property reflects the number of elements (last index + 1).
- Modifying `length` can truncate the array.

**Additional Methods:**

- **Adding/Removing Elements:**
  - `push(...items)`: Adds items to the end of the array.
  - `pop()`: Removes and returns the last element from the array.
  - `shift()`: Removes and returns the first element from the array.
  - `unshift(...items)`: Adds items to the beginning of the array.
  - `splice(start, deleteCount, ...items)`: Inserts or removes elements from a specific index.
- **Searching:**
  - `indexOf/lastIndexOf(item, pos)`: Searches for an item and returns its index.
  - `includes(value)`: Checks if the array contains a value.
  - `find(func)`: Returns the first element that meets a condition.
  - `filter(func)`: Creates a new array with elements that meet a condition.
  - `findIndex(func)`: Returns the index of the first element that meets a condition (similar to `find` but returns index).
- **Iterating:**
  - `forEach(func)`: Calls a function for each element in the array.
- **Transforming:**
  - `map(func)`: Creates a new array with the results of calling a function on each element.
  - `sort(func)`: Sorts the array in place.
  - `reverse()`: Reverses the order of the elements in the array.
  - `join(glue)`: Joins all elements into a string.
  - `split(delimiter)`: Splits a string into an array of substrings.
  - `reduce(func, initial)`: Applies a function against an accumulator and each element in the array to reduce it to a single value.
- **Other Useful Methods:**
  - `Array.isArray(value)`: Checks if a value is an array.
  - `concat(...items)`: Creates a new array by merging existing arrays or values.
  - `some(func)`: Checks if at least one element in the array passes a test.
  - `every(func)`: Checks if all elements in the array pass a test.
  - `fill(value, start, end)`: Fills all or part of the array with a static value.
  - `copyWithin(target, start, end)`: Copies a section of the array within itself.
  - `flat(depth)/flatMap(fn)`: Creates a new array from a multidimensional array (advanced).
