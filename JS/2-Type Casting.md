# Type Casting

Type casting means conversion of one data type to another explicitly. In JavaScript some of the most common methods to convert a datatype to either string using `String()`, to boolean using `Boolean()`, or to number using `Number()`.

- **Type conversion**

  - Type conversion (or typecasting) means transfer of data from one data type to another.

- **Type coercion**

  - Type coercion is the automatic or implicit conversion of values from one data type to another (such as strings to numbers)

- **Examples**

```js
// Define a constant variable named value1 and assign the string "5" to it.
const value1 = "5";

// Define a constant variable named value2 and assign the number 9 to it.
const value2 = 9;

// Declare a variable named sum and initialize it with the result of adding value1 and value2.
// Note that since value1 is a string, attempting to add it to a number (value2)
// will result in concatenating the two values.
let sum = value1 + value2;

// Print the value of the sum variable to the console.
console.log(sum);
```

---

## Implicit and Explicit type casting

**Implicit**
In implicit type casting, the programming language automatically converts data from one type to another if needed.

**Explicit**
Explicit type casting, also known as type conversion or type coercion, occurs when the programmer explicitly converts a value from one data type to another.
