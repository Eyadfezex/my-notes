# setTimeout

The setTimeout runs a function after the specified period expires. Times are declared in milliseconds.

```js
function sayHi() {
  console.log("Hello World!");
}

// Call the function after 2 seconds (2000 milliseconds)
setTimeout(sayHi, 2000);

console.log("This will be shown first.");
```
