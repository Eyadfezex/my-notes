# Stacks

Stacks: **LIFO** (Last In, First Out) Data Structures

Stacks are a type of data structure that follow a specific order for adding and removing elements: LIFO (Last In, First Out). Think of a stack of plates - you can only add a new plate on top and can only remove the plate from the top.

- **Adding elements (push):** New elements are added to the "top" of the stack.
- **Removing elements (pop):** Elements are removed from the "top" of the stack.

**Implementation:**

Stacks can be implemented using arrays or linked lists. The provided example uses a linked list for better clarity.

**Example Uses:**

- **Function calls:** Keeping track of function calls in programs.
- **Undo/redo functionality:** Reversing actions in software.
- **Expression evaluation:** Processing mathematical expressions.

**Performance:**

- **Insertion (push):** O(1) - Constant time, fast.
- **Removal (pop):** O(1) - Constant time, fast.
- **Searching:** O(n) - Linear time, can be slow for larger stacks.
- **Access:** O(n) - Linear time, can be slow for larger stacks (because you might need to traverse down the stack to find a specific element).

```js
// Simple stack using an array

class Stack {
  constructor() {
    this.items = []; // Initialize an empty array to store the stack elements
  }

  // Push a new element onto the stack
  push(element) {
    this.items.push(element);
  }

  // Pop the top element from the stack and return it
  pop() {
    if (this.isEmpty()) {
      return null; // Indicate stack is empty
    }
    return this.items.pop();
  }

  // Check if the stack is empty
  isEmpty() {
    return this.items.length === 0;
  }
}

// Create a stack
const myStack = new Stack();

// Push some elements
myStack.push("apple");
myStack.push("banana");
myStack.push("orange");

// Pop elements and print them
console.log(myStack.pop()); // Output: orange
console.log(myStack.pop()); // Output: banana
console.log(myStack.pop()); // Output: apple

// Check if the stack is empty
console.log(myStack.isEmpty()); // Output: true
```
