# Imperative vs Declarative

Imperative programming is **how** you do something, and declarative programming is more like **what** you do.

The imperative approach is concerned with **how** you’re actually going to do something. You need to list out the steps to be able to show **how** you’re going to to do what you want. The declarative approach is more concerned with **what** you want, i want something.

---

## IMPERATIVE

- C
- C++
- Java

## DECLARATIVE

- HTML
- SQL

## ~BOTH

- JavaScript
- C#
- Python

Think about your typical SQL or HTML code,

```sql
SELECT \* FROM Users WHERE Country='Mexico';
```

```html
<article>
  <header>
    <h1>Declarative Programming</h1>
    <p>Sprinkle Declarative in your verbiage to sound smart</p>
  </header>
</article>
```

Both examples are declarative, focusing on **what** needs to be done rather than **how** to do it. They describe the desired outcome without specifying implementation details, abstracting away concerns such as parsing HTML or querying a database.

Here is the interview-type question. We're going to answer it **imperatively**, as if we're focused on **how**.

Write a function called `double` which takes in an array of numbers and returns a new array after doubling every item in that array – `double([1,2,3]) // [2,4,6]`.

```js
function double(arr) {
let results = [];
for (let i = 0; i < arr.length; i++) {
results.push(arr[i] \* 2);
}
return results;
}
```

Here is the **declarative** answer for the same question.

```js
function double(arr) {
  return arr.map((item) => item * 2);
}
```

In the declarative example, we specify **what** we want to achieve, not **how**. Implementation details like map and reduce are abstracted away, with no state mutation. This enhances readability, especially once familiar with map and reduce.

---

### some definitions

- `Declarative programming is “the act of programming in languages that conform to the mental model of the developer rather than the operational model of the machine.”`

---

- `In computer science, declarative programming is a programming paradigm that expresses the logic of a computation without describing its control flow.`
