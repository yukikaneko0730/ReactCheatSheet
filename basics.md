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

```
---

## 🔑 Props

Props let you pass data from parent to child.

```jsx
function Welcome(props) {
  return <h2>Welcome, {props.user}!</h2>;
}

<Welcome user="Alice" />

````
👉 Props are read-only. You cannot modify them inside the child component.

