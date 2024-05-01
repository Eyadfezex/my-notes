# `this`

In JavaScript, the `this` keyword is a little different compared to other languages. It refers to an object, but it depends on how or where it is being invoked. It also has some differences between strict mode and non-strict mode.

In non–strict mode, `this` is always a reference to an object. In strict mode, it can be any value. For more information on how the value is determined, see the description below.

```js
const test = {
  prop: 42,
  func: function () {
    return this.prop;
  },
};

console.log(test.func());
// Expected output: 42

//---------------------------------

function getThis() {
  return this;
}

const obj1 = { name: "obj1" };
const obj2 = { name: "obj2" };

obj1.getThis = getThis;
obj2.getThis = getThis;

console.log(obj1.getThis()); // { name: 'obj1', getThis: [Function: getThis] }
console.log(obj2.getThis()); // { name: 'obj2', getThis: [Function: getThis] }
```

---

## Function Borrowing in JavaScript

Function borrowing in JavaScript is a technique that allows you to use a method defined on one object with another object. It's a way to share functionality without relying on inheritance or copying the function itself.

**Borrowing Mechanisms:**

- `call()`: `This` method allows you to explicitly set the `this` keyword for the function call. You pass the object you want to use as `this` as the first argument, followed by any other arguments the function expects.

- `apply()`: Similar to `call()`, but it takes arguments as an array instead of individual parameters.

- `bind()`: This method creates a new function with a pre-defined `this` value. You can then call the bound function with any arguments needed.

```js
function greet() {
  console.log("Hello, my name is " + this.name);
}

const person1 = { name: "Alice" };
const person2 = { name: "Bob" };

greet.call(person1); // Outputs: Hello, my name is Alice
greet.apply(person2); // Outputs: Hello, my name is Bob

const boundGreetAlice = greet.bind(person1);
boundGreetAlice(); // Outputs: Hello, my name is Alice
```

---

The `this` keyword in JavaScript is context-sensitive. Here's a concise breakdown:

**Methods:** Inside an object's method, `this` refers to the object itself.

**Regular Functions:**

- **Alone:** `this` refers to the global object (window) or is `undefined` in strict mode.
- **With `call()` / `apply()`:** You can set `this` explicitly for the function call.

```js
const button = document.getElementById("myButton");

button.addEventListener("click", function () {
  console.log("The button with ID " + this.id + " was clicked!");
});

// Here, this refers to the button element that triggered the click event.
```

**Event Handlers:** `this` refers to the DOM element that triggered the event.

**Arrow Functions:** `this` inherits from the surrounding context, so use with caution in methods.
