# Pass props to Link

In React Router, you define routes that map URLs to specific components in your application. These components often need additional data to function properly, such as user information, product IDs, or specific views to display.

You directly define the component element to render. Pass props just like any other React component:

```tsx
<Route
  path="/products/:productId"
  element={<ProductDetails productId={productId} />}
/>
```

To get the prop from the URL we use [`useParams`](../Router%20Hooks/useParams.md) react-router-dom Hook
