# JSON (JavaScript Object Notation)

JSON (JavaScript Object Notation) is a text-based data exchange format. It is a collection of key-value pairs where the key must be a string type, and the value can be of any of the following types: (Number,String,Boolean,Array,Object,null)

**Example:**

```json
{
  "name": "Alex C",
  "age": 2,
  "city": "Houston"
}
```

**Valid JSON data can be in two different formats:**

A collection of key-value pairs enclosed by a pair of curly braces `{...}`. You saw this as an example above.
A collection of an ordered list of key-value pairs separated by comma (,) and enclosed by a pair of square brackets `[...]`. See the example below:

```json
[
  {
    "name": "Alex C",
    "age": 2,
    "city": "Houston"
  },
  {
    "name": "John G",
    "age": 40,
    "city": "Washington"
  },
  {
    "name": "Bala T",
    "age": 22,
    "city": "Bangalore"
  }
]
```

---

## JavaScript Objects and JSON are NOT the Same

The JSON data format is derived from the JavaScript object structure. But the similarity ends there.

Objects in JavaScript:

- Can have methods, and JSON can't.
- The keys can be without quotes.
- Comments are allowed.
- Are JavaScript's own entity.
