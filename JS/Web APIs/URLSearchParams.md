# URLSearchParams

The `URLSearchParams` interface defines utility methods to work with the query string of a URL.

## Constructor

The`URLSearchParams()`constructor creates and returns a new `URLSearchParams` object.

### Syntax

```js
new URLSearchParams();
new URLSearchParams(options);
```

### Example

```js
// Retrieve params via url.search, passed into constructor
const url = new URL("https://example.com?foo=1&bar=2");
const params1 = new URLSearchParams(url.search);

// Get the URLSearchParams object directly from a URL object
const params1a = url.searchParams;

// Pass in a string literal
const params2 = new URLSearchParams("foo=1&bar=2");
const params2a = new URLSearchParams("?foo=1&bar=2");

// Pass in a sequence of pairs
const params3 = new URLSearchParams([
  ["foo", "1"],
  ["bar", "2"],
]);

// Pass in a record
const params4 = new URLSearchParams({ foo: "1", bar: "2" });
```
