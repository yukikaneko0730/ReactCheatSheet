# 🧩 React Patterns

This section covers **common React patterns** that improve reusability, maintainability, and clarity in code.  
These are not frameworks — just proven ways to structure components and logic. 

---

## 📦 Container & Presentational Components

**Separate logic from UI.**

```jsx
// Presentational (dumb) component
const UserList = ({ users }) => (
  <ul>
    {users.map((u) => (
      <li key={u.id}>{u.name}</li>
    ))}
  </ul>
);

// Container (smart) component
function UserListContainer() {
  const [users, setUsers] = React.useState([]);

  React.useEffect(() => {
    fetch("/api/users")
      .then((res) => res.json())
      .then(setUsers);
  }, []);

  return <UserList users={users} />;
}
```

---

## Controlled vs. Uncontrolled Components

*Controlled* → React manages the value.
*Uncontrolled* → DOM manages the value (via ref).

```jsx
// Controlled
function ControlledInput() {
  const [value, setValue] = React.useState("");
  return <input value={value} onChange={(e) => setValue(e.target.value)} />;
}

// Uncontrolled
function UncontrolledInput() {
  const inputRef = React.useRef();
  const handleSubmit = () => alert(inputRef.current.value);
  return (
    <>
      <input ref={inputRef} />
      <button onClick={handleSubmit}>Submit</button>
    </>
  );
}
```

---

## 🔑 Lifting State Up

Move state to a common parent so children can share it.

```jsx
function Parent() {
  const [text, setText] = React.useState("");

  return (
    <>
      <ChildInput text={text} setText={setText} />
      <ChildDisplay text={text} />
    </>
  );
}

const ChildInput = ({ text, setText }) => (
  <input value={text} onChange={(e) => setText(e.target.value)} />
);

const ChildDisplay = ({ text }) => <p>{text}</p>;
```

---

## 📡 Prop Drilling vs. Context

*Prop Drilling (bad if too deep*)*:
```jsx
<GrandParent>
  <Parent>
    <Child theme="dark" />
  </Parent>
</GrandParent>
```
*Context (better):*
```jsx
const ThemeContext = React.createContext("light");

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Child />
    </ThemeContext.Provider>
  );
}

function Child() {
  const theme = React.useContext(ThemeContext);
  return <p>Theme: {theme}</p>;
}
```

---

## 🧱 Compound Components

Let components work together in a flexible API.

```jsx
function Tabs({ children }) {
  const [active, setActive] = React.useState(0);

  return (
    <div>
      {React.Children.map(children, (child, i) =>
        React.cloneElement(child, { active, setActive, index: i })
      )}
    </div>
  );
}

const Tab = ({ active, setActive, index, children }) => (
  <button onClick={() => setActive(index)}>
    {active === index ? <b>{children}</b> : children}
  </button>
);

// Usage
<Tabs>
  <Tab>Tab 1</Tab>
  <Tab>Tab 2</Tab>
</Tabs>
```

---

## 🪢 Render Props

Pass a function as a prop to share logic.

```jsx
const MouseTracker = ({ children }) => {
  const [pos, setPos] = React.useState({ x: 0, y: 0 });
  return (
    <div onMouseMove={(e) => setPos({ x: e.clientX, y: e.clientY })}>
      {children(pos)}
    </div>
  );
};

// Usage
<MouseTracker>
  {({ x, y }) => <p>Mouse at {x}, {y}</p>}
</MouseTracker>
```

---

## 🧩 Higher-Order Components (HOC)

A function that takes a component and returns a new component.

```jsx
function withLogger(Component) {
  return function Wrapped(props) {
    console.log("Props:", props);
    return <Component {...props} />;
  };
}

const Hello = ({ name }) => <h1>Hello {name}</h1>;

const HelloWithLogger = withLogger(Hello);
```

---

## 🪄 Custom Hooks as Patterns

Encapsulate logic in a hook to reuse across components.

```jsx
function useFetch(url) {
  const [data, setData] = React.useState(null);

  React.useEffect(() => {
    fetch(url).then((res) => res.json()).then(setData);
  }, [url]);

  return data;
}

// Usage
const users = useFetch("/api/users");
```

---

## 📦 Container & Presentational Components

Separate logic from UI.

```jsx
// Presentational (dumb) component
const UserList = ({ users }) => (
  <ul>
    {users.map((u) => (
      <li key={u.id}>{u.name}</li>
    ))}
  </ul>
);

// Container (smart) component
function UserListContainer() {
  const [users, setUsers] = React.useState([]);

  React.useEffect(() => {
    fetch("/api/users")
      .then((res) => res.json())
      .then(setUsers);
  }, []);

  return <UserList users={users} />;
}
```

---

🟢 Controlled vs. Uncontrolled Components

```jsx
// Controlled
function ControlledInput() {
  const [value, setValue] = React.useState("");
  return <input value={value} onChange={(e) => setValue(e.target.value)} />;
}

// Uncontrolled
function UncontrolledInput() {
  const inputRef = React.useRef();
  const handleSubmit = () => alert(inputRef.current.value);
  return (
    <>
      <input ref={inputRef} />
      <button onClick={handleSubmit}>Submit</button>
    </>
  );
}
```

---

## 🔑 Lifting State Up

Move state to a common parent so children can share it.

```jsx
function Parent() {
  const [text, setText] = React.useState("");

  return (
    <>
      <ChildInput text={text} setText={setText} />
      <ChildDisplay text={text} />
    </>
  );
}

const ChildInput = ({ text, setText }) => (
  <input value={text} onChange={(e) => setText(e.target.value)} />
);

const ChildDisplay = ({ text }) => <p>{text}</p>;
```

---

## 📡 Prop Drilling vs. Context

```jsx
const ThemeContext = React.createContext("light");

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Child />
    </ThemeContext.Provider>
  );
}

function Child() {
  const theme = React.useContext(ThemeContext);
  return <p>Theme: {theme}</p>;
}
```

---

## 🧱 Compound Components
```jsx
function Tabs({ children }) {
  const [active, setActive] = React.useState(0);

  return (
    <div>
      {React.Children.map(children, (child, i) =>
        React.cloneElement(child, { active, setActive, index: i })
      )}
    </div>
  );
}

const Tab = ({ active, setActive, index, children }) => (
  <button onClick={() => setActive(index)}>
    {active === index ? <b>{children}</b> : children}
  </button>
);

// Usage
<Tabs>
  <Tab>Tab 1</Tab>
  <Tab>Tab 2</Tab>
</Tabs>
```

---

## 🪢 Render Props

```jsx
const MouseTracker = ({ children }) => {
  const [pos, setPos] = React.useState({ x: 0, y: 0 });
  return (
    <div onMouseMove={(e) => setPos({ x: e.clientX, y: e.clientY })}>
      {children(pos)}
    </div>
  );
};

// Usage
<MouseTracker>
  {({ x, y }) => <p>Mouse at {x}, {y}</p>}
</MouseTracker>
```

---

## 🧩 Higher-Order Components (HOC)
```jsx
function withLogger(Component) {
  return function Wrapped(props) {
    console.log("Props:", props);
    return <Component {...props} />;
  };
}

const Hello = ({ name }) => <h1>Hello {name}</h1>;

const HelloWithLogger = withLogger(Hello);
```

---

## 🪄 Custom Hooks as Patterns
```jsx
function useFetch(url) {
  const [data, setData] = React.useState(null);

  React.useEffect(() => {
    fetch(url).then((res) => res.json()).then(setData);
  }, [url]);

  return data;
}
```

---

## ⚡ Performance Patterns

**🧊 React.memo**

Prevent re-render if props don’t change.

```jsx
const Child = React.memo(({ value }) => {
  console.log("Rendered");
  return <p>{value}</p>;
});
```


**🧮 useMemo**

Cache expensive calculations.

```jsx
const total = useMemo(() => items.reduce((a, b) => a + b, 0), [items]);
```


**🪢 useCallback**

Cache functions to avoid unnecessary re-renders.

```jsx
const handleClick = useCallback(() => console.log("clicked"), []);
```


**💤 Lazy Loading & Suspense**

Split code and load components only when needed.

```jsx
const HeavyComponent = React.lazy(() => import("./HeavyComponent"));

<Suspense fallback={<p>Loading...</p>}>
  <HeavyComponent />
</Suspense>
```


**🧯 Error Boundaries**

Catch errors gracefully.

```jsx
class ErrorBoundary extends React.Component {
  state = { hasError: false };
  static getDerivedStateFromError() {
    return { hasError: true };
  }
  render() {
    return this.state.hasError ? <h2>Something went wrong.</h2> : this.props.children;
  }
}
```

---

✨ **Quick Recap**

- **Container & Presentational** → Separate logic from UI  
- **Controlled vs. Uncontrolled** → React-managed vs. DOM-managed inputs  
- **Lifting State Up** → Share state via parent  
- **Prop Drilling vs. Context** → Avoid passing props too deeply  
- **Compound Components** → Flexible APIs with nested components  
- **Render Props** → Share logic via a function prop  
- **HOC (Higher-Order Components)** → Wrap components with extra functionality  
- **Custom Hooks** → Reuse logic across components  
- **Performance Patterns** →  
  - **React.memo** → Prevent re-renders  
  - **useMemo** → Cache expensive calculations  
  - **useCallback** → Cache functions  
  - **lazy + Suspense** → Load code on demand  
  - **Error Boundaries** → Catch runtime errors gracefully  

