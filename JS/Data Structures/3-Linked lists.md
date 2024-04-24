# Linked lists

## Linked Lists vs. Arrays

- **Structure:** Linked lists store data in nodes, each containing a value and a pointer to the next node. Arrays use contiguous memory locations for elements.
- **Indexing:** Linked lists lack direct indexing like arrays. You traverse the list to find elements.
- **Insertion/Deletion:** Insertion/deletion in linked lists is generally faster as you only need to adjust pointers. In arrays, elements might need to be shifted.

---

**Single List** :

- ![single list](https://www.freecodecamp.org/news/content/images/2022/05/linked-list.png)

---

**double List** :

- ![double list](https://www.freecodecamp.org/news/content/images/2022/05/doubly-linked-list.png)

---

### Singly Linked List Implementation

The provided code implements a singly linked list with methods like `push`, `pop`, `shift`, `unshift`, `get`, `set`, `insert`, `remove`, and `reverse`. Here's a summary of their functionalities:

- `push`: Adds a new element to the end of the list.
- `pop`: Removes the last element from the list.
- `shift`: Removes the first element from the list.
- `unshift`: Adds a new element to the beginning of the list.
- `get`: Retrieves the element at a specific index (linear time).
- `set`: Modifies the value of an element at a specific index (linear time).
- `insert`: Inserts a new element at a specific index.
- `remove`: Removes an element at a specific index.
- `reverse`: Reverses the order of elements in the list.

### Time Complexities

- **Insertion:** O(1) - Constant time, efficient due to pointer manipulation.
- **Removal:** O(n) - Linear time, may require iterating to find the element.
- **Search:** O(n) - Linear time, similar to removal.
- **Access:** O(n) - Linear time, no direct indexing like arrays.

```js
class Node {
  constructor(val) {
    this.val = val;
    this.next = null;
    this.prev = null; // This is the key difference for doubly linked lists
  }
}

class DoublyLinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this.length = 0;
  }

  // Similar methods to singly linked list for push, pop, shift, unshift

  // Get method with slight modification to handle traversing backwards
  get(index) {
    if (index < 0 || index >= this.length) return null;
    let current;
    let count = 0;
    if (index <= this.length / 2) {
      current = this.head;
      while (count < index) {
        current = current.next;
        count++;
      }
    } else {
      current = this.tail;
      count = this.length - 1;
      while (count > index) {
        current = current.prev;
        count--;
      }
    }
    return current;
  }

  // Set method remains similar

  // Insert method with additional logic to update pointers for previous and next nodes
  insert(index, val) {
    if (index < 0 || index > this.length) return false;
    if (index === this.length) return !!this.push(val);
    if (index === 0) return !!this.unshift(val);

    const newNode = new Node(val);
    if (!this.head) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      const prevNode = this.get(index - 1);
      const nextNode = prevNode.next;
      prevNode.next = newNode;
      newNode.prev = prevNode;
      newNode.next = nextNode;
      nextNode.prev = newNode;
    }
    this.length++;
    return true;
  }

  // Remove method with similar logic to update pointers for previous and next nodes
  remove(index) {
    if (index < 0 || index >= this.length) return undefined;
    if (index === 0) return this.shift();
    if (index === this.length - 1) return this.pop();

    const removedNode = this.get(index);
    const prevNode = removedNode.prev;
    const nextNode = removedNode.next;
    prevNode.next = nextNode;
    nextNode.prev = prevNode;
    this.length--;
    return removedNode;
  }
}
```
