# Queues

Queues: **FIFO** (First In, First Out) Data Structures

Queues are similar to stacks but maintain a different order for adding and removing elements. They follow the FIFO (First In, First Out) principle. Imagine a line at a store - the first person in line is the first person served.

- **Adding elements (enqueue):** New elements are added to the "back" of the queue.
- **Removing elements (dequeue):** Elements are removed from the "front" of the queue.

**Implementation:**

Queues can be implemented using arrays or linked lists. The provided example uses a linked list for better clarity.

**Example Uses:**

- **Background tasks:** Queues can be used to manage tasks that run in the background, ensuring they are processed in the order they are added.
- **Printing/task processing:** Queues can be used to manage print jobs or other tasks that need to be completed in a specific order.

**Performance:**

- **Insertion (enqueue):** O(1) - Constant time, fast.
- **Removal (dequeue):** O(1) - Constant time, fast.
- **Searching:** O(n) - Linear time, can be slow for larger queues.
- **Access:** O(n) - Linear time, can be slow for larger queues (because you might need to traverse down the queue to find a specific element).

**Key Points:**

- Queues ensure elements are processed in the order they are added.
- They are useful for scenarios where a first-come, first-served approach is needed.

```js
// Queue using a linked list

class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class Queue {
  constructor() {
    this.first = null;
    this.last = null;
    this.size = 0;
  }

  // Enqueue a new element to the back of the queue
  enqueue(value) {
    const newNode = new Node(value);
    if (!this.first) {
      this.first = newNode;
      this.last = newNode;
    } else {
      this.last.next = newNode;
      this.last = newNode;
    }
    this.size++;
  }

  // Dequeue the element from the front of the queue and return it
  dequeue() {
    if (!this.first) return null;
    const temp = this.first;
    if (this.first === this.last) {
      this.last = null;
    }
    this.first = this.first.next;
    this.size--;
    return temp.value;
  }

  // Check if the queue is empty
  isEmpty() {
    return this.size === 0;
  }
}

// Create a queue
const myQueue = new Queue();

// Enqueue some elements
myQueue.enqueue("apple");
myQueue.enqueue("banana");
myQueue.enqueue("orange");

// Dequeue elements and print them
console.log(myQueue.dequeue()); // Output: apple
console.log(myQueue.dequeue()); // Output: banana
console.log(myQueue.dequeue()); // Output: orange

// Check if the queue is empty
console.log(myQueue.isEmpty()); // Output: true
```
