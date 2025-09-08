# 🪝 React Hooks

This section covers the **most commonly used React Hooks** — the core of modern React development.  
Hooks let you use state, lifecycle methods, and more without writing class components. 

---

## 🟢 useState

Manage local component state.

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      Count: {count}
    </button>
  );
}
```

---

## 🔄 useEffect

Perform side effects (fetch data, update title, set timers).

```jsx
import { useEffect, useState } from "react";

function Example() {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch("/api/data")
      .then((res) => res.json())
      .then(setData);

    return () => console.log("Cleanup on unmount");
  }, []); // Empty dependency array → run once
}
```

---

## 🧱 useContext

Access context values without prop drilling.

```jsx
import { createContext, useContext } from "react";

const ThemeContext = createContext("light");

function Child() {
  const theme = useContext(ThemeContext);
  return <div>Theme: {theme}</div>;
}

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Child />
    </ThemeContext.Provider>
  );
}
```

---

## ⚙️ useReducer

An alternative to useState for more complex state logic.

```jsx
import { useReducer } from "react";

const reducer = (state, action) => {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    default:
      return state;
  }
};

function Counter() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <button onClick={() => dispatch({ type: "increment" })}>
      {state.count}
    </button>
  );
}
```

---

## 🪞 useRef

Keep values between renders or reference DOM elements.

```jsx
import { useRef } from "react";

function InputFocus() {
  const inputRef = useRef();

  return (
    <>
      <input ref={inputRef} />
      <button onClick={() => inputRef.current.focus()}>
        Focus Input
      </button>
    </>
  );
}
```

---

## 🧮 useMemo

Memoize expensive calculations.

```jsx
import { useMemo, useState } from "react";

function ExpensiveCalculation({ items }) {
  const total = useMemo(
    () => items.reduce((sum, i) => sum + i, 0),
    [items]
  );

  return <p>Total: {total}</p>;
}
```
---

## 🪢 useCallback

Memoize functions to prevent unnecessary re-renders.

```jsx
import { useState, useCallback } from "react";

function Parent() {
  const [count, setCount] = useState(0);

  const increment = useCallback(() => {
    setCount((c) => c + 1);
  }, []);

  return <Child onClick={increment} />;
}

function Child({ onClick }) {
  return <button onClick={onClick}>Increment</button>;
}
```

---

## ⏳ useLayoutEffect (Advanced)

Like useEffect but runs synchronously after DOM mutations.
Useful for measuring DOM size before the browser repaints.

```jsx
import { useLayoutEffect, useRef } from "react";

function Measure() {
  const boxRef = useRef();

  useLayoutEffect(() => {
    console.log(boxRef.current.getBoundingClientRect());
  }, []);

  return <div ref={boxRef}>Measure me</div>;
}
```

---

## 🎣 Custom Hooks

Create your own reusable hooks (prefix with use).

```jsx
import { useState, useEffect } from "react";

function useWindowSize() {
  const [size, setSize] = useState({
    width: window.innerWidth,
    height: window.innerHeight,
  });

  useEffect(() => {
    const handleResize = () =>
      setSize({ width: window.innerWidth, height: window.innerHeight });

    window.addEventListener("resize", handleResize);
    return () => window.removeEventListener("resize", handleResize);
  }, []);

  return size;
}

// Usage
const { width, height } = useWindowSize();
```

---

## 🎭 useImperativeHandle

Customize the instance value exposed when using ref with forwardRef.

```jsx
import { useRef, forwardRef, useImperativeHandle } from "react";

const CustomInput = forwardRef((_, ref) => {
  const inputRef = useRef();

  useImperativeHandle(ref, () => ({
    focus: () => inputRef.current.focus(),
  }));

  return <input ref={inputRef} />;
});

function App() {
  const ref = useRef();
  return (
    <>
      <CustomInput ref={ref} />
      <button onClick={() => ref.current.focus()}>Focus Input</button>
    </>
  );
}
```

---

## ⏩ useTransition (React 18+)

Handle state updates with lower priority → improves UI responsiveness.

```jsx
import { useState, useTransition } from "react";

function Search() {
  const [query, setQuery] = useState("");
  const [isPending, startTransition] = useTransition();

  const handleChange = (e) => {
    const value = e.target.value;
    startTransition(() => {
      setQuery(value);
    });
  };

  return (
    <div>
      <input onChange={handleChange} />
      {isPending ? <p>Loading...</p> : <p>Result for: {query}</p>}
    </div>
  );
}
```

---

## 🕒 useDeferredValue (React 18+)

Defer expensive rendering until later (great for search results).

```jsx
import { useState, useDeferredValue } from "react";

function SearchList({ items }) {
  const [query, setQuery] = useState("");
  const deferredQuery = useDeferredValue(query);

  const filtered = items.filter((i) =>
    i.toLowerCase().includes(deferredQuery.toLowerCase())
  );

  return (
    <>
      <input value={query} onChange={(e) => setQuery(e.target.value)} />
      <ul>{filtered.map((i) => <li key={i}>{i}</li>)}</ul>
    </>
  );
}

```

---

##🔄 useId (React 18+)

Generate stable unique IDs for accessibility attributes.

```jsx
import { useId } from "react";

function Form() {
  const id = useId();
  return (
    <>
      <label htmlFor={id}>Name:</label>
      <input id={id} type="text" />
    </>
  );
}
```

---

## 🛠 useDebugValue (for custom hooks)

Add labels to custom hooks for debugging in React DevTools.

```jsx
import { useDebugValue, useState } from "react";

function useOnlineStatus() {
  const [online, setOnline] = useState(true);
  useDebugValue(online ? "Online ✅" : "Offline ❌");
  return online;
}
```

---

✨ **Quick Recap**

- 🟢 **useState** → Manage local state  
- 🔄 **useEffect** → Side effects (fetch, subscriptions, cleanup)  
- 🧱 **useContext** → Share state without prop drilling  
- ⚙️ **useReducer** → Complex state logic (like Redux in a component)  
- 🪞 **useRef** → Persist values & access DOM elements  
- 🧮 **useMemo** → Memoize expensive calculations  
- 🪢 **useCallback** → Memoize functions to avoid re-renders  
- ⏳ **useLayoutEffect** → Sync DOM reads/writes before paint  
- 🎣 **Custom Hooks** → Reusable logic across components  
- 🎭 **useImperativeHandle** → Expose custom APIs via `ref`  
- ⏩ **useTransition** → Prioritize urgent vs. non-urgent updates  
- 🕒 **useDeferredValue** → Defer heavy updates for smoother typing  
- 🔄 **useId** → Generate unique IDs (accessibility, forms)  
- 🛠 **useDebugValue** → Debug custom hooks in DevTools  





