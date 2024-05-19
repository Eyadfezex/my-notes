# GSAP ScrollTrigger: Breathe Life into Your Scrolling Experience

GSAP ScrollTrigger is a powerful extension for the GSAP animation library, allowing you to create dynamic, scroll-based animations. Imagine elements smoothly fading in, translating across the screen, or revealing themselves with parallax effects as users scroll!

**Key Features and Controls:**

- **Trigger:** (**required**) This is the reference point for the animation. It can be a DOM element, selector string, or even the entire viewport (`window`).
- **Start & End:** Define when the animation begins and concludes relative to the trigger's scroll position. Use percentages, viewport positions (like "top bottom"), or specific scroll targets (e.g., "#element + 100").
- **Scrub:** Links the progress of the animation directly to the scrollbar so it acts like a scrubber. You can apply smoothing so that it takes a little time for the playhead to catch up with the scrollbar's position! It can be any of the following

**Beyond the Basics:**

- **Pin:** (boolean) Fix an element to a specific position as the user scrolls (great for creating sticky headers or sidebars).
- **pinType:** ("fixed" or "transform") Choose how the pinning works: fixed relative to the viewport or translated within its container.
- **Markers:** (boolean) Enable visual markers to see the animation's scroll trigger zones for easy debugging.
- **Callbacks:** Utilize functions like `onUpdate` for dynamic adjustments on every scroll update, `onEnter` for actions when the animation enters the viewport, and `onLeave` for actions when it leaves.

**Resources:**

- **Official Documentation:** [ScrollTrigger](https://gsap.com/docs/v3/Plugins/ScrollTrigger/)

**Example (React with react-gsap):**

```jsx
import React, { useRef } from "react";
import { useGSAP } from "react-gsap";

const AnimatedBox = () => {
  const boxRef = useRef(null);

  const tl = useGSAP({
    from: { x: 0 }, // Initial state (optional)
    to: { x: 500 }, // Animation properties
    scrollTrigger: {
      trigger: boxRef.current, // Element that triggers the animation
      start: "top bottom", // Animation starts when top reaches bottom of viewport
    },
  });

  return (
    <div ref={boxRef} className="box">
      This element will be animated on scroll!
    </div>
  );
};

export default AnimatedBox;
```
