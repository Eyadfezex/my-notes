# Outlet

An `<Outlet>` should be used in parent route elements to render their child route elements.

This allows nested UI to show up when child routes are rendered. If the parent route matched exactly, it will render a child index route or nothing if there is no index route.

## Syntax

```jsx
function component() {
  return (
    <div>
      <h1>Dashboard</h1>

      {/* This element will render either <DashboardMessages> when the URL is
          "/messages", <DashboardTasks> at "/tasks", or null if it is "/"
      */}
      <Outlet />
    </div>
  );
}

function App() {
  return (
    <Routes>
      <Route path="/" element={<Dashboard />}>
        <Route path="messages" element={<DashboardMessages />} />
        <Route path="tasks" element={<DashboardTasks />} />
        <Route>
      <Route  element={<component />}>
        <Route path="messages" element={<component_1 />} />
        <Route path="tasks" element={<component_2 />} />

        </Route>
      </Route>
    </Routes>
  );
}
```
