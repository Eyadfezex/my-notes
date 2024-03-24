# `useSearchParams`

The `useSearchParams` hook is used to read and modify the query string in the URL for the current location.

Just as React's `useState` hook, `setSearchParams` also supports **functional updates**. Therefore, you may provide a function that takes a searchParams and returns an updated version.

## Return

Like React's own `useState` hook, `useSearchParams` returns an array of **two values**:

- the current location's search params
- function that may be used to update them.

### Syntax

```jsx
import { useSearchParams } from 'react-router-dom'

const Results = () => {
  const [searchParams, setSearchParams] = useSearchParams();

  const q = searchParams.get('q')
  const src = searchParams.get('src')
  const f = searchParams.get('f')

  return (
    ...
  )
}

// ------------------------------------------------------

import { useSearchParams } from 'react-router-dom'

const Results = () => {
  const [searchParams, setSearchParams] = useSearchParams();

  const q = searchParams.get('q')
  const src = searchParams.get('src')
  const f = searchParams.get('f')

  const updateOrder = (sort) => {
    setSearchParams({ sort })
  }

  return (
    ...
  )
}
```
