# Objects: the basics

objects are used to store keyed collections of various data and more complex entities. In **JavaScript**, objects penetrate almost every aspect of the language.

An object can be created with figure brackets `{…}` with an optional list of properties. A property is a “key: value” pair, where `key` is a string (also called a “property name”), and `value` can be anything.

An empty object (“empty cabinet”) can be created using one of two syntaxes:

```js
let user = new Object(); // "object constructor" syntax
let user = {}; // "object literal" syntax
```

## Square brackets

For **multiword** properties, the dot access doesn’t work:

```js
let user = {};

// set
user["likes birds"] = true;

// get
alert(user["likes birds"]); // true

// delete
delete user["likes birds"];
```

## Property value shorthand

In JavaScript, when creating object properties with the same name as their corresponding variable, you can leverage property value shorthand for a concise syntax. This eliminates the need for explicit property name repetition.

```js
function makeUser(name, age) {
  return {
    name: name,
    age: age,
    // ...other properties
  };
}

let user = makeUser("John", 30);
alert(user.name); // John
```

### Operators

- `in`
  Checks if a specific property exists within an object. Returns true if the property exists, false otherwise.

  ```js
  const person = { name: "Charlie" };
  console.log("name" in person); // Output: true
  console.log("age" in person); // Output: false
  ```

- `delete`
  Removes a property from an object. Returns `true` if the property is deleted successfully, `false` otherwise.

  ```js
  const person = { name: "David" };
  delete person.name;
  console.log("name" in person); // Output: false (property deleted)
  ```

- **Comparison Operators (`==`, `!=`, `===`, `!==`, `<`, `>`, `<=`, `>=`)**
  Used to compare object properties or entire objects for equality or order. However, direct object comparison with `==` or `!=` is generally not recommended as it might lead to unexpected results due to reference equality vs. value equality.

  ```js
  const person1 = { name: "Alice" };
  const person2 = { name: "Alice" }; // Different objects with same values

  console.log(person1 == person2); // Might be false due to reference equality
  console.log(person1.name === person2.name); // Recommended for value comparison
  ```

- `typeof`
  Returns the data type of an object. Useful for checking if a variable holds an object.

  ```js
  const person = {};
  console.log(typeof person); // Output: object
  ```

### Object prototype

In JavaScript, every object you create implicitly has a prototype. This prototype acts as a template that defines properties and methods the object can inherit. You can think of it as the object's DNA.

**Example:**

```JavaScript
function Car(color, model) {
this.color = color;
this.model = model;
}

Car.prototype.startEngine = function() {
console.log("Engine started for " + this.model);
};

const blueHonda = new Car("blue", "Honda Civic");

console.log(blueHonda.color); // "blue" inherited from Car prototype

blueHonda.startEngine(); // "Engine started for Honda Civic"

console.log(blueHonda.__proto__); // Shows the Car prototype object
```

### Prototypal inheritance

Prototypal inheritance is a fundamental mechanism in JavaScript that allows objects to inherit properties and methods from other objects. It differs from class-based inheritance found in languages like Java or C++.

```js
let animal = {
  eats: true,
};
let rabbit = {
  jumps: true,
};

rabbit.__proto__ = animal; // (*)

// we can find both properties in rabbit now:
alert(rabbit.eats); // true (**)
alert(rabbit.jumps); // true
```
