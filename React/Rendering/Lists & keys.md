# Lists & keys

In React, lists are used to render multiple elements dynamically based on an array of data.

Keys are special attributes used in React when rendering lists of elements. They help React identify which items have changed, are added, or are removed from the list.

## Lists

Lists in React are created by mapping over an array of data and returning a component for each item in the array. For example:

```jsx
const items = ["apple", "banana", "orange"];

const ListComponent = () => (
  <ul>
    {items.map((item, index) => (
      <li key={index}>{item}</li>
    ))}
  </ul>
);
```

## Keys

Keys in React are special identifiers used to efficiently update lists by identifying changes, additions, or removals. They help React optimize DOM manipulations. Providing a unique key is Important, preferably using stable IDs from your data for dynamic lists. For example :

```jsx
const items = [
  { id: 1, name: "apple" },
  { id: 2, name: "banana" },
  { id: 3, name: "orange" },
];

const ListComponent = () => (
  <ul>
    {items.map((item) => (
      <li key={item.id}>{item.name}</li>
    ))}
  </ul>
);
```
