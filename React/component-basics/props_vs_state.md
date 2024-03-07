## Props and State in React

Props and state are both core concepts in React used for managing data within components, but they serve different purposes.

### Props (Properties)

- Props are short for properties.
- They are inputs to a React component.
- They are passed from parent components down to child components.
- Props are immutable, meaning they cannot be modified by the component receiving them.
- They are used to customize or configure a component's behavior and appearance.

### State

- State represents the internal data of a component.
- Unlike props, which are passed in from the outside, state is managed internally within the component.
- State can be modified using the `setState()` method provided by React.
- Changes to state trigger re-rendering of the component and its children.
- State is typically used for dynamic data that can change over time, such as user input, fetched data, or component-specific UI state.
