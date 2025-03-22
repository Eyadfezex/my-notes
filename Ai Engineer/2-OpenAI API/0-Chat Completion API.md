# Chat Completion API

## **Endpoint**

- `POST /v1/chat/completions`

## **Request Parameters**

- `model`: Model name (e.g., `"gpt-3.5-turbo"`).
- `messages`: Array of `{ role: "system" | "user" | "assistant", content: "text" }`.
- `temperature` (optional): Controls randomness (0-2).
- `top_p` (optional): Nucleus sampling (0-1).
- `max_tokens` (optional): Limit response length.
- `stop` (optional): Stop sequence(s).
- `user` (optional): Unique user ID for abuse monitoring.

## **Response Structure**

- `id`: Completion ID.
- `model`: Model used.
- `choices`: Array of responses `{ message: { role, content }, finish_reason }`.
- `usage`: `{ prompt_tokens, completion_tokens, total_tokens }`.

## **Example Request (JavaScript)**

```js
fetch("https://api.openai.com/v1/chat/completions", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    Authorization: "Bearer YOUR_API_KEY",
  },
  body: JSON.stringify({
    model: "gpt-3.5-turbo",
    messages: [{ role: "user", content: "Hello!" }],
    temperature: 0.7,
  }),
})
  .then((res) => res.json())
  .then((data) => console.log(data))
  .catch((err) => console.error(err));
```

For full details, visit [OpenAI API Docs](https://platform.openai.com/docs/api-reference/chat).
