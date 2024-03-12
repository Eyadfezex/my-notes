# useCallback Hook

`useCallback` is a React Hook that lets you cache a function definition between re-renders.

- `useCallback(fn, dependencies)`

## Parameters

- `fn`: The function value that you want to cache.
- `dependencies`:he list of all reactive values referenced inside of the `fn` code.

## Returns

- On the initial render, useCallback returns the fn function you have passed.
