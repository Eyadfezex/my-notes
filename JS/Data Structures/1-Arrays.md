# Arrays

In JavaScript, arrays store collections of items and let you access them by **position**. JavaScript arrays are cool! Unlike some languages, they can mix data types and grow/shrink on the fly, making them handy for various data.

```js
const arr = ["a", "b", "c", "d"];
console.log(arr[2]); // c

//--------------------------------------------------------

const arr = ["store", 1, "whatever", 2, "you want", 3];
```

---

## Objects

JavaScript objects store data like a dictionary. They use key-value pairs to organize information, making them perfect for situations where data has a natural relationship.

```js
const person = {
  firstName: "Alice",
  lastName: "Smith",
  age: 30,
  introduceSelf: function () {
    console.log(`Hi! My name is ${this.firstName} ${this.lastName}.`);
  },
};

// Access properties
console.log(person.firstName); // Output: Alice
console.log(person["age"]); // Output: 30

// Call a method
person.introduceSelf(); // Output: Hi! My name is Alice Smith.
```
