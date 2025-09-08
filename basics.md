# ⚛️ React Basics

This section covers the **fundamentals of React** — JSX, props, state, and rendering.  
Perfect for a quick refresher or for beginners starting with React. 

---

## 📦 Components

React components are the building blocks of the UI.

```jsx
// Function component
function Hello({ name }) {
  return <h1>Hello, {name}!</h1>;
}

// Usage
<Hello name="Yuki" />

```
---

## 🔑 Props

Props let you pass data from parent to child.

```jsx
function Welcome(props) {
  return <h2>Welcome, {props.user}!</h2>;
}

<Welcome user="Alice" />

```
👉 Props are read-only. You cannot modify them inside the child component.

---

## 🟢 State

State allows components to store and update data internally.

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

## 🔁 Rendering Lists

Use .map() with a unique key.

```jsx
const items = ["Apple", "Banana", "Cherry"];

<ul>
  {items.map((item, index) => (
    <li key={index}>{item}</li>
  ))}
</ul>
```

---

## 🎭 Conditional Rendering

Render UI based on conditions.

```jsx
{isLoggedIn ? <Dashboard /> : <Login />}
{isAdmin && <AdminPanel />}
```

---

## 🎨 Styling

Inline styles, CSS modules, or utility frameworks like Tailwind.

```jsx
<div style={{ color: "red", fontSize: 18 }}>
  Inline styled text
</div>
```

---

## # ⚛️ React Basics

This section covers the **fundamentals of React** — JSX, props, state, and rendering.  
Perfect for a quick refresher or for beginners starting with React. 🚀

---

## 📦 Components

React components are the building blocks of the UI.

```jsx
// Function component
function Hello({ name }) {
  return <h1>Hello, {name}!</h1>;
}

// Usage
<Hello name="Yuki" />

```
---

## 🔑 Props

Props let you pass data from parent to child.

```jsx
function Welcome(props) {
  return <h2>Welcome, {props.user}!</h2>;
}

<Welcome user="Alice" />

```
👉 Props are read-only. You cannot modify them inside the child component.

---

## 🟢 State

State allows components to store and update data internally.

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

## 🔁 Rendering Lists

Use .map() with a unique key.

```jsx
const items = ["Apple", "Banana", "Cherry"];

<ul>
  {items.map((item, index) => (
    <li key={index}>{item}</li>
  ))}
</ul>
```

---

## 🎭 Conditional Rendering

Render UI based on conditions.

```jsx
{isLoggedIn ? <Dashboard /> : <Login />}
{isAdmin && <AdminPanel />}
```

---

## 🎨 Styling

Inline styles, CSS modules, or utility frameworks like Tailwind.

```jsx
<div style={{ color: "red", fontSize: 18 }}>
  Inline styled text
</div>
```

---

## 📝 JSX Rules

JSX has a few important rules:

```jsx
// Only one parent element is allowed
return (
  <div>
    <h1>Hello</h1>
    <p>World</p>
  </div>
);

// Attributes use camelCase
<input type="text" onChange={handleChange} />

// JavaScript expressions inside {}
<p>{2 + 2}</p>
```

---

## 🧱 Fragments

Avoid unnecessary <div> wrappers by using fragments.

```jsx
return (
  <>
    <h1>Title</h1>
    <p>Description</p>
  </>
);
```

---

## 🔄 Events

Handle user interactions with event handlers.

```jsx
<button onClick={() => alert("Clicked!")}>
  Click me
</button>

<form onSubmit={(e) => { e.preventDefault(); console.log("Submitted!"); }}>
  <input type="text" />
  <button type="submit">Submit</button>
</form>
```

---

## 📦 Imports & Exports

Module basics in React:

```jsx
// default export
export default function App() { ... }

// named export
export function Header() { ... }

// import
import App from "./App";
import { Header } from "./Header";
```

---

## 🟣 Default Props

Give props default values when not provided.

```jsx
function Button({ label = "Click me" }) {
  return <button>{label}</button>;
}

// Usage
<Button /> // → renders "Click me"
<Button label="Submit" /> // → renders "Submit"
```

---

## 🟤 Destructuring Props

A cleaner way to use props inside components.

```jsx
function Profile({ name, age }) {
  return <p>{name} is {age} years old.</p>;
}

<Profile name="Alice" age={25} />
```

---

## 👶 Children Prop

Allows components to wrap other content.

```jsx
function Card({ children }) {
  return <div className="card">{children}</div>;
}

// Usage
<Card>
  <h2>Title</h2>
  <p>Content inside card</p>
</Card>
```

---

## 🟡 Rendering Nothing (null)

Return null if you don’t want to render anything.

```jsx
function HiddenMessage({ show }) {
  if (!show) return null;
  return <p>Secret revealed!</p>;
}
```

---

## 🗝️ Keys Best Practice

Use a unique id instead of array index for lists.

```jsx
const items = [
  { id: 1, name: "Apple" },
  { id: 2, name: "Banana" }
];

<ul>
  {items.map((item) => (
    <li key={item.id}>{item.name}</li>
  ))}
</ul>

```

---

## 🗂️ File Naming Convention (Optional)

Follow React conventions for file names.

✔️ Good:  MyComponent.jsx
❌ Bad:   mycomponent.jsx

---




✨ **Quick Recap**

- **Components** → Reusable UI building blocks  
- **Props** → Pass data from parent to child (read-only)  
- **State** → Internal, mutable data for dynamic UI  
- **Lists** → Use `.map()` with a unique `key`  
- **Conditional Rendering** → Render with `? :` or `&&`  
- **JSX** → One parent element, camelCase attributes, `{}` for JS expressions  
- **Fragments** → Use `<> ... </>` instead of unnecessary `<div>`  
- **Events** → Common handlers like `onClick`, `onSubmit`, etc.  
- **Imports/Exports** → Organize modules with `default` and `named` exports  
- **Default Props** → Provide fallback values for props  
- **Children Prop** → Pass nested content between component tags  
- **Keys** → Prefer stable unique IDs over array indexes  
