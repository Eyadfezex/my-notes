# GSAP Methods: Bringing Your Animations to Life

GSAP provides a powerful set of methods for creating and controlling animations on your web pages. Here's a look at some core methods to get you started:

**Core Animation Methods:**

- **[`gsap.to()`](<[https://gsap.com/docs/v3/GSAP/gsap.to](https://gsap.com/docs/v3/GSAP/gsap.to)()>):** This method creates a "tween" animation, smoothly transitioning a target element from its current state to a specified end state. You can animate various properties like position, rotation, opacity, and more.

  Example:

  ```javascript
  // Rotate and move elements with a class of "box" over 1 second.
  gsap.to(".box", { rotation: 27, x: 100, duration: 1 });
  ```

- **[`gsap.from()`](<[https://gsap.com/docs/v3/GSAP/gsap.from](https://gsap.com/docs/v3/GSAP/gsap.from)()>):** Similar to `gsap.to()`, this method animates from a starting state to an ending state. It's useful for creating animations that reveal elements or bring them into focus.

  Example:

  ```javascript
  // Animate elements with class ".class" from an initial opacity of 0 and a y position of 100 (like being off-screen)
  // to their current on-screen positions (opacity of 1 and y position of 0).
  gsap.from(".class", { opacity: 0, y: 100, duration: 1 });
  ```

- **[`gsap.fromTo()`](<[https://gsap.com/docs/v3/GSAP/gsap.fromTo](https://gsap.com/docs/v3/GSAP/gsap.fromTo)()>):** This method combines the functionality of `gsap.from()` and `gsap.to()` in one step. You define both the starting and ending states for the animation.

  Example:

  ```javascript
  // Animate elements with class ".class" from an initial opacity of 0 and a y position of 100 (like being off-screen)
  // to their current on-screen positions (opacity of 1 and y position of 0). (Equivalent to the previous gsap.from() example)
  gsap.fromTo(
    ".class",
    { opacity: 0, y: 100 },
    { opacity: 1, y: 0, duration: 1 }
  );
  ```

- **[`gsap.timeline()`](<[https://gsap.com/docs/v3/GSAP/gsap.timeline](https://gsap.com/docs/v3/GSAP/gsap.timeline)()>):** This method creates a timeline object, allowing you to sequence and synchronize multiple animations. Timelines provide fine-grained control over the flow and timing of your animations.

  **Example without Timelines (using delays):**

  ```javascript
  // This approach requires manual delays between animations.
  gsap.to("#id", { x: 100, duration: 1 });
  gsap.to("#id", { y: 50, duration: 1, delay: 1 }); // Wait 1 second
  gsap.to("#id", { opacity: 0, duration: 1, delay: 2 }); // Wait 2 seconds
  ```

  **Example with Timelines (cleaner and more versatile):**

  ```javascript
  // Timelines offer centralized control and easier sequencing.
  var tl = gsap.timeline({ repeat: 2, repeatDelay: 1 }); // Repeat animation twice with a 1-second delay between loops
  tl.to("#id", { x: 100, duration: 1 });
  tl.to("#id", { y: 50, duration: 1 });
  tl.to("#id", { opacity: 0, duration: 1 });

  // Now you can easily control the entire animation sequence:
  tl.pause(); // Pause the animation
  tl.resume(); // Resume the animation
  tl.seek(1.5); // Jump to the 1.5-second mark in the animation
  tl.reverse(); // Play the animation in reverse
  ```

By effectively combining these core methods and GSAP's extensive animation options, you can create dynamic and engaging animations for your web projects.
