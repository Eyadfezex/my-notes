# Catch all (404) Pages

All you have to do is render a `Route` with a `path` of `*`, and React Router will make sure to only render the `element` if none of the other Routes match.

## Example

```jsx
<Routes>
  <Route path="*" element={<NotFound />} />
  <Route path="/" element={<Home />} />
  <Route path="/about" element={<About />} />
  <Route path="/settings" element={<Settings />} />
</Routes>
```
