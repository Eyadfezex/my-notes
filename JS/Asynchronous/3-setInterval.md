# setInterval

`setInterval` is a built-in function in JavaScript that repeatedly executes a function or code block at a specified time interval. It's like a loop that keeps running the code at regular intervals until you explicitly stop it.
**Syntax**

```js
const intervalID = setInterval(functionToRun, milliseconds);
clearInterval(intervalID);
```

- `intervalID`: The variable to store the returned ID for later use with `clearInterval`.
- `functionToRun`: The function you want to execute repeatedly.
- `milliseconds`: The delay between each execution (in milliseconds).

```js
function displayTime() {
  const date = new Date();
  const time = date.toLocaleTimeString();
  console.log(time);
}

const intervalID = setInterval(displayTime, 1000); // Call every 1 second
```
