# Three Principles

Here's a simplified explanation of the three core principles in Redux:

1. **One Big Box (Single Source of Truth):**  
   Imagine all your application's data lives in a single box. This makes it easier to manage and keeps everything organized.

2. **Actions Tell the Box What to Do (State is Read-Only):**  
   Components can't directly change things in the box. Instead, they send messages (actions) describing what needs to happen (like "add a todo").

3. **Pure Functions Update the Box (Changes are Made with Pure Functions):**  
   Special functions (reducers) take the current state of the box and the action message, then return a brand new box with the updates. This ensures everything is predictable and easy to debug.
