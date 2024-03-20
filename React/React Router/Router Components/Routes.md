# Routes

You can think of `Routes` as the metaphorical conductor of your `route`s.

Whenever you have one or more Routes, you'll most likely want to wrap them in a `Routes`.The reason for this is because it's Routes job is to understand all of its children Route elements, and intelligently choose which ones are the best to render.

- Example :

````jsx
import { Routes, Route } from "react-router-dom";

function App() {
  return (
    <Routes>
      <Route path="/" element={<Home />} />
      <Route path="/about" element={<About />} />
      <Route path="/settings" element={<Settings />} />
      <Route path="*" element={<NotFound />} />
    </Routes>
  );
}```
````
