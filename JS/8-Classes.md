# Classes in JavaScript

JavaScript classes provide a structured approach to object-oriented programming, offering a blueprint for creating objects with similar properties and behaviors.

**Key Concepts:**

- **Class Definition:** Classes are declared using the `class` keyword followed by the class name. They serve as templates for creating objects.

  ```javascript
  class Car {
    // ... properties and methods
  }
  ```

- **Constructor Method:** A special method called automatically when a new object (instance) is created from the class. Its primary purpose is to initialize object properties.

  ```javascript
  class Car {
    constructor(make, model, year) {
      this.make = make;
      this.model = model;
      this.year = year;
    }
  }

  const myCar = new Car("Ford", "Mustang", 2023);
  ```

- **Class Methods:** Functions defined within the class to encapsulate behavior related to the object. These methods can be invoked on instances of the class.

  ```javascript
  class Car {
    constructor(make, model, year) {
      // ...
    }

    accelerate() {
      console.log("Car is accelerating!");
    }
  }

  myCar.accelerate(); // Calls the accelerate method on the myCar instance
  ```

- **Inheritance:** Classes can inherit properties and methods from other classes, promoting code reuse and creating hierarchical relationships.

  ```javascript
  class ElectricCar extends Car {
    constructor(make, model, year, batteryRange) {
      super(make, model, year); // Call parent class constructor
      this.batteryRange = batteryRange;
    }

    charge() {
      console.log("Electric car is charging!");
    }
  }

  const electricCar = new ElectricCar("Tesla", "Model S", 2024, 400);
  electricCar.accelerate(); // Inherited from Car
  electricCar.charge(); // Specific to ElectricCar
  ```

- **Static Methods:** Functions attached directly to the class itself, callable without creating an instance. They typically operate on the class itself or perform utility functions.

  ```javascript
  class Car {
    // ...

    static compareYears(car1, car2) {
      return car1.year - car2.year;
    }
  }

  const ageDifference = Car.compareYears(myCar, electricCar);
  ```

- **Getter and Setter Methods:** Allow custom control over how properties are accessed and modified. Getters are invoked when a property is read, while setters are called when a property is assigned a new value.

  ```javascript
  class Person {
    constructor(firstName, lastName) {
      this._fullName = `${firstName} ${lastName}`; // Private property
    }

    get fullName() {
      // Getter method
      return this._fullName;
    }

    set fullName(newName) {
      // Setter method
      this._fullName = newName.toUpperCase(); // Enforce uppercase
    }
  }

  const person = new Person("John", "Doe");
  console.log(person.fullName); // Uses getter
  person.fullName = "Jane Smith"; // Uses setter (name will be uppercase)
  ```

**Example:**

```javascript
class Shape {
    constructor(color) {
        this.color = color;
    }

    getArea() {
        throw new Error("getArea() is not implemented for this shape!");
    }
}

// Mark Shape as abstract
abstract class Shape {}

class Square extends Shape {
    constructor(color, sideLength) {
        super(color); // Call parent constructor
        this.sideLength = sideLength;
    }

    getArea() {
        return this.sideLength * this.sideLength;
    }
}

const square = new Square("red", 5);
console.log(`Area of the square: ${square.getArea()}`);
```

**Additional Notes:**

- Classes in JavaScript are a syntactic sugar on top of the prototype-based inheritance model.
- Understanding prototypes is still essential for a deeper grasp of object-oriented programming in JavaScript.
