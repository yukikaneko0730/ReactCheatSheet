# 🛠 React Tips & Tricks

This section covers **useful tips, patterns, and best practices** that make React development smoother and safer. 🚀

---

## 🔑 Conditional Class Names

Switch styles dynamically.

```jsx
<div className={isActive ? "text-blue-500" : "text-gray-500"}>
  {isActive ? "Active" : "Inactive"}
</div>
```
👉 With clsx library:

```bash
npm install clsx
```
```jsx
import clsx from "clsx";

<div className={clsx("p-2", isActive && "bg-green-200")}>
  Hello
</div>
```

---

## 🕒 Debounce & Throttle

Limit how often a function is called.

```bash
npm install lodash
```

```jsx
import { debounce } from "lodash";

const handleSearch = debounce((text) => {
  console.log("Searching:", text);
}, 500);

<input onChange={(e) => handleSearch(e.target.value)} />
```

---

## 💾 Local Storage Hook

Persist state between reloads.

```jsx
function useLocalStorage(key, initial) {
  const [value, setValue] = React.useState(() =>
    JSON.parse(localStorage.getItem(key)) ?? initial
  );

  React.useEffect(() => {
    localStorage.setItem(key, JSON.stringify(value));
  }, [key, value]);

  return [value, setValue];
}

// Usage
const [theme, setTheme] = useLocalStorage("theme", "light");
```

---

## 🛑 Event Propagation

Stop events from bubbling up.

```jsx
<div onClick={() => console.log("Outer clicked")}>
  <button onClick={(e) => e.stopPropagation()}>
    Inner button
  </button>
</div>
```

---

## ⌨️ Keyboard Events

Handle global key presses.

```jsx
React.useEffect(() => {
  const handleKey = (e) => {
    if (e.key === "Escape") console.log("Escape pressed");
  };
  window.addEventListener("keydown", handleKey);
  return () => window.removeEventListener("keydown", handleKey);
}, []);
```

---

## 🌀 Abort Fetch Requests

Prevent memory leaks in async calls.

```jsx
React.useEffect(() => {
  const controller = new AbortController();

  fetch("/api/data", { signal: controller.signal })
    .then((res) => res.json())
    .then(console.log)
    .catch((err) => {
      if (err.name !== "AbortError") throw err;
    });

  return () => controller.abort();
}, []);
```

---

## 📦 Env Variables

Store secrets and configs safely.

```bash
.env
REACT_APP_API_URL=https://api.example.com
```

```jsx
const url = process.env.REACT_APP_API_URL;
```

---

## 🔍 Debugging Tools

**React DevTools** → Inspect components & state

**why-did-you-render** → Detect unnecessary renders

**eslint-plugin-react** → Enforce best practices

---

✨ **Quick Recap**

- **Conditional Class Names** → Switch styles dynamically  
- **Debounce & Throttle** → Limit frequent calls  
- **Local Storage Hook** → Persist state across reloads  
- **Event Propagation** → Stop bubbling with `stopPropagation()`  
- **Keyboard Events** → Handle global key presses  
- **Abort Fetch** → Cancel requests on unmount  
- **Env Variables** → Store API keys/config safely  
- **Debugging Tools** → DevTools, ESLint, performance helpers  
