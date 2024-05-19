# Gsap props

In GSAP, props refer to the properties you specify within animation methods like `gsap.to()`, `gsap.from()`, and others, that define what and how you want to animate. These props determine the target element's characteristics that will change during the animation.

- **Target Properties:** These props specify the CSS properties of the element you want to animate. Some common examples include:
  - `x`, `y`: for animating position
  - `opacity`: for fading elements
  - `width`, `height`: for resizing elements
  - `rotation`, `scaleX`, `scaleY`: for transforming elements
  - Any other valid CSS property can also be animated with GSAP.
- **Animation Options:** These props control the overall behavior of the animation, such as:
  - `duration`: Sets the animation length in seconds.
  - `ease`: Selects an easing function to determine the animation's timing curve (e.g., ease in, ease out).
  - `delay`: Defines a delay before the animation starts.
  - `repeat`: Sets the number of times to repeat the animation.
  - `yoyo`: Controls whether the animation should play forward and then backward.
  - There are many other animation options available in GSAP.

**Using Props:**

Props are passed as an object within the animation method. Here's an example:

```javascript
gsap.to(".my-element", {
  x: 200, // Animate the element's x position to 200px (Target Property)
  duration: 2, // Animation Option (duration)
  ease: "power3.out", // Animation Option (ease)
});
```

In this case, the target property is `x` and the animation options are `duration` and `ease`.

---

## Stagger

The `stagger` prop in GSAP is specifically used for creating staggered animations. It allows you to animate multiple elements with a slight delay between each, creating a cascading or wave-like effect.

**Usage:**

The `stagger` prop is typically used within the animation methods like `gsap.to()`, `gsap.from()`, or `gsap.fromTo()`. It's included as part of an object containing the animation properties.

Here's the basic syntax:

```javascript
gsap.to(".my-elements", {
  // Other animation properties...
  stagger: value
}, ...);
```

**Stagger Value:**

The `value` you provide for `stagger` determines the delay between each element's animation. It can be:

- **Number:** A positive number represents the delay (in seconds) between each element's animation start. For example, `stagger: 0.2` would create a 0.2-second delay between each element.
- **Object:** For more control, you can use an object to define the stagger behavior:
  - `each`: (Number) Similar to a numeric value, defines the delay between elements.
  - `from`: (String, "center", "start", or "end") Specifies the starting point of the stagger. "center" staggers outwards from the center element, "start" staggers from the first element, and "end" staggers from the last element.
  - `axis`: (String, "x" or "y") Restricts the stagger to a specific axis (horizontal or vertical). By default, it applies to both axes (x and y).

**Examples:**

```js
gsap.to(".box", {
  x: 100,  // Animate all elements to x position 100px
  opacity: 1, // Animate opacity to 1 (from 0 or initial state)
  duration: 1,
  stagger: 0.3  // Delay each element by 0.3 seconds
}, ...);
```

```js
gsap.to(".box", {
  // Move all elements with class ".box" down by 100px
  y: 100,

  // Apply stagger animation with advanced options
  stagger: {
    // Delay each element by 0.1 seconds
    each: 0.1,

    // Stagger animation from the center outwards
    from: "center",

    // Arrange elements in a grid-like layout (determined by available space)
    grid: "auto",

    // Use power2.inOut easing function for a smooth animation curve
    ease: "power2.inOut",

    // Repeat the animation infinitely (can be adjusted)
    repeat: -1,
  },
});
```
