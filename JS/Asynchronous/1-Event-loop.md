# Event-loop

The event loop allows Node to perform non-blocking I/O operations despite the fact that JavaScript is single-threaded. It is done by assigning operations to the operating system whenever and wherever possible.

- **Call Stack:** Think of this as a stack of plates where each plate represents a function being executed. The loop processes functions one at a time, following the order they were called.
  ![s](https://res.cloudinary.com/practicaldev/image/fetch/s--Kn5tSJEm--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_800/https://devtolydiahallie.s3-us-west-1.amazonaws.com/gid1.6.gif)
- **Event Queue:** This is a queue where asynchronous operations like timers (setTimeout), user interactions (clicks, key presses), and Web API callbacks are placed.
  ![s](https://res.cloudinary.com/practicaldev/image/fetch/s--fqt0UJmH--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_800/https://devtolydiahallie.s3-us-west-1.amazonaws.com/gif2.1.gif)
  ![s](https://res.cloudinary.com/practicaldev/image/fetch/s--qxI9YF9R--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_800/https://devtolydiahallie.s3-us-west-1.amazonaws.com/gif3.1.gif)
- **Event Loop:** This loop continuously performs these actions:
  - Checks if the call stack is empty.
  - If empty, it pulls the next function from the event queue and pushes it onto the call stack for execution.
  - If the call stack is not empty, it continues executing the current function on the stack.
    ![s](https://res.cloudinary.com/practicaldev/image/fetch/s--OIG-_8dF--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_800/https://devtolydiahallie.s3-us-west-1.amazonaws.com/gif4.gif)

---

**Let's quickly take a look at what's happening when we're running this code in a browser:**
![s](https://res.cloudinary.com/practicaldev/image/fetch/s--dhjH4Wt---/c_limit%2Cf_auto%2Cfl_progressive%2Cq_66%2Cw_800/https://devtolydiahallie.s3-us-west-1.amazonaws.com/gif14.1.gif)
