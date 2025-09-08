# ⚛️ React Basics

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

---

## 🔑 Props

Props let you pass data from parent to child.

```jsx
function Welcome(props) {
  return <h2>Welcome, {props.user}!</h2>;
}

<Welcome user="Alice" />

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

---

## 🎭 Conditional Rendering

Render UI based on conditions.

```jsx
{isLoggedIn ? <Dashboard /> : <Login />}
{isAdmin && <AdminPanel />}

---

## 🎨 Styling

Inline styles, CSS modules, or utility frameworks like Tailwind.

```jsx
<div style={{ color: "red", fontSize: 18 }}>
  Inline styled text
</div>



