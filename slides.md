---
theme: default
---

# Introduction to React Hooks

---

## `useState` Hook

- `useState` is a hook provided by React for managing state in Function components.
- It allows you to add state to function components without converting them to class components.
- It returns a stateful value and a function to update it.
- Functional updates can be used to update state based on the previous state.

---

## `useState` Example

```js
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  const increment = () => {
    setCount((prevCount) => prevCount + 1);
  };

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={increment}>Increment</button>
    </div>
  );
}
```

---

## `useEffect` Hook

- `useEffect` is a hook provided by React for handling side effects in functional components.
- It allows you to perform side effects in function components similar to lifecycle methods in class components.
- It runs after every render by default.
- Cleanup can be performed by returning a function from the effect.

---

## useEffect ex1

```js
import React, { useState, useEffect } from 'react';

function DataFetcher() {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch('https://api.example.com/data')
      .then((response) => response.json())
      .then((data) => setData(data))
      .catch((error) => console.error('Error fetching data:', error));
  }, []);

  return <div>{data ? <p>Data: {data}</p> : <p>Loading...</p>}</div>;
}
```

---

## `useEffect` ex2

```js
import React, { useState, useEffect } from 'react';

function Timer() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    const intervalId = setInterval(() => {
      setCount((count) => count + 1);
    }, 1000);

    return () => clearInterval(intervalId);
  }, []);

  return (
    <div>
      <p>Count: {count}</p>
    </div>
  );
}
```

---

## useEffect ex3

```js
import React, { useState, useEffect } from 'react';

function MouseTracker() {
  const [position, setPosition] = useState({ x: 0, y: 0 });

  useEffect(() => {
    const updateMousePosition = (e) => {
      setPosition({ x: e.clientX, y: e.clientY });
    };

    window.addEventListener('mousemove', updateMousePosition);

    return () => {
      window.removeEventListener('mousemove', updateMousePosition);
    };
  }, []);

  return (
    <div>
      <p>
        Mouse position: {position.x}, {position.y}
      </p>
    </div>
  );
}
```

---

## useReducer Hook

- `useReducer` is a hook provided by React for managing complex state logic in functional components.
- It is an alternative to `useState` when the state logic is more complex and involves multiple sub-values or when the next state depends on the previous one.
- It is suitable for scenarios where the state logic is more complex and involves multiple sub-values.
- It follows the reducer pattern similar to Redux.

---

## useReducer ex1

```js
import React, { useReducer } from 'react';

const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      throw new Error('Unsupported action type');
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'increment' })}>Increment</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>Decrement</button>
    </div>
  );
}
```

---
layout: two-cols
---

## useReducer ex2

```js
import React, { useReducer } from 'react';

const initialState = {
  loading: false,
  error: null,
  data: null,
};

function reducer(state, action) {
  switch (action.type) {
    case 'FETCH_REQUEST':
      return { ...state, loading: true };
    case 'FETCH_SUCCESS':
      return { ...state, loading: false, data: action.payload };
    case 'FETCH_ERROR':
      return { ...state, loading: false, error: action.payload };
    default:
      throw new Error('Unsupported action type');
  }
}
```

::right::

```js
function DataFetcher() {
  const [state, dispatch] = useReducer(reducer, initialState);

  useEffect(() => {
    dispatch({ type: 'FETCH_REQUEST' });
    fetch('https://api.example.com/data')
      .then((response) => response.json())
      .then((data) => dispatch({ type: 'FETCH_SUCCESS', payload: data }))
      .catch((error) => dispatch({ type: 'FETCH_ERROR', payload: error }));
  }, []);

  return (
    <div>
      {state.loading ? (
        <p>Loading...</p>
      ) : state.error ? (
        <p>Error: {state.error.message}</p>
      ) : (
        <p>Data: {state.data}</p>
      )}
    </div>
  );
}
```

---

## useRef Hook

- Exploring the useRef hook for accessing DOM elements and persisting values across renders.
- Use cases for useRef, including accessing and modifying DOM elements imperatively.
- How useRef can be used to store mutable values without causing re-renders.
- Practical examples demonstrating useRef usage.

---

## useMemo Hook

- Understanding the useMemo hook for memoizing expensive computations.
- Explanation of when to use useMemo to optimize performance.
- Syntax and usage of useMemo hook.
- Examples illustrating useMemo for optimizing computations in functional components.

---

## useCallback Hook

- Introduction to the useCallback hook for memoizing callback functions.
- Understanding when to use useCallback to prevent unnecessary re-renders.
- Syntax and usage of useCallback hook.
- Examples demonstrating useCallback for optimizing callback functions in functional components.

---

## useContext Hook

- Introduction to the useContext hook for accessing context in functional components.
- Explanation of context and its role in React applications.
- How to consume context values using useContext.
- Real-world examples showcasing useContext for managing application-wide state.

---

# Conclusion

- Recap of the covered React Hooks.
- Importance of understanding and leveraging hooks for building efficient React applications.
- Further resources for diving deeper into React Hooks.
