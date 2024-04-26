# Loop statements

Loops can execute a block of code a number of times.

- `for` : The `for` statement defines a code block that is executed as long as a condition is `true`.

```js
for (let i = 0; i < 5; i++) {
  text += i; // 0 1 2 3 4
}
```

---

- `do...while`: The `do...while` statements combo defines a code block to be executed once, and repeated as long as a condition is `true`.

```js
let text = "";
let i = 0;
do {
  text += i;
  i++;
} while (i < 5); // 0 1 2 3 4
```

---

- `while`: The `while` statement creates a loop (around a code block) that is executed while a condition is `true`.

```js
let text = "";
let i = 0;
while (i < 5) {
  text += i;
  i++;
} // 0 1 2 3 4
```

---

- `for...in`: The `for...in` statements combo iterates (loops) over the properties of an object.

```js
const person = { fname: "John", lname: "Doe", age: 25 };
let text = "";
for (let x in person) {
  text += person[x] + " "; //John Doe 25
}
```

---

- `for...of`: The `for...of` statements combo iterates (loops) over the values of any iterable.

```js
let text = "";
const cars = ["BMW", "Volvo", "Mini"];
for (let x of cars) {
  text += x + " ";
} // BMW Volvo Mini
```

---

- `break` :The break statement breaks out of a switch or a loop, In a switch, it breaks out of the switch block. This stops the execution of more code inside the switch, In in a loop, it breaks out of the loop and continues executing the code after the loop (if any).

```js
let text = "";
for (let i = 0; i < 5; i++) {
  if (i === 3) break;
  text += i + "<br>";
} // 0 1 2;
```

- `continue`: The `continue` statement breaks one iteration (in the loop), if a specified condition occurs, and continues with the next iteration in the loop.

```js
or (let i = 0; i < 5; i++) {
  if (i === 3) { continue; }
  text +=i; //0 1 2 3 4
}
```
