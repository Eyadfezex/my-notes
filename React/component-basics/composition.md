# Composition in React

Composition is a fundamental concept in React that involves combining multiple components together to create more complex UI structures. It enables developers to build reusable and modular components by composing smaller, simpler components together.

![composition](../../img/react-components@1.5x.svg)

## How Composition Works

In React, components can be composed in several ways:

1. **Using Props**: Components can be composed by passing props to child components, allowing them to customize behavior or appearance.

2. **Nesting Components**: Components can be nested within each other, creating a hierarchy of components where child components are encapsulated within parent components.

3. **Higher-Order Components (HOCs)**: HOCs are functions that accept a component as input and return a new enhanced component with additional functionality.

4. **Render Props**: Render props is a pattern where a component's render method receives a function as a prop, which it then calls to render its content. This allows for greater flexibility and reusability.

## Benefits of Composition

- **Reusability**: Composition encourages building smaller, reusable components that can be combined in different ways to create new functionality.
- **Modularity**: Components can be broken down into smaller, more manageable pieces, making code easier to understand and maintain.
- **Flexibility**: Composition allows for greater flexibility in building UIs, as components can be mixed and matched to create complex structures.
- **Separation of Concerns**: By composing components, concerns such as data fetching, styling, and logic can be separated into distinct components, improving code organization and readability.

## Example

```jsx
import React from "react";
import Header from "./Header";
import Sidebar from "./Sidebar";
import MainContent from "./MainContent";

function App() {
  return (
    <div>
      <Header />
      <div className="container">
        <Sidebar />
        <MainContent />
      </div>
    </div>
  );
}

export default App;
```
