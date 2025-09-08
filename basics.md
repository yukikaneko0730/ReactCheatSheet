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