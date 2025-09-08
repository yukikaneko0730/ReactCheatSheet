# 📘 React + TypeScript Cheat Sheet

A quick reference for using **TypeScript with React (TSX)** —  
covering props, state, events, refs, context, and custom hooks. 🚀

---

## 🔑 Typed Props

```tsx
type WelcomeProps = {
  user: string;
  age?: number; // optional
};

function Welcome({ user, age }: WelcomeProps) {
  return <h2>Welcome, {user} {age && `(${age})`}</h2>;
}

// Usage
<Welcome user="Alice" age={25} />
```

---

## 🟢 useState with Types

```tsx
const [count, setCount] = React.useState<number>(0);
const [items, setItems] = React.useState<string[]>([]);
```

---

## 🪞 useRef with Types

```tsx
const inputRef = React.useRef<HTMLInputElement>(null);

<input ref={inputRef} />
<button onClick={() => inputRef.current?.focus()}>Focus</button>
```

---

## 🔄 Event Handlers

```tsx
const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
  console.log(e.target.value);
};

const handleSubmit = (e: React.FormEvent<HTMLFormElement>) => {
  e.preventDefault();
  console.log("Submitted!");
};

<form onSubmit={handleSubmit}>
  <input type="text" onChange={handleChange} />
  <button type="submit">Send</button>
</form>
```

---

## 🧱 Function Components

```tsx
import React, { FC } from "react";

type ButtonProps = {
  label: string;
  onClick: () => void;
};

const Button: FC<ButtonProps> = ({ label, onClick }) => (
  <button onClick={onClick}>{label}</button>
);
```
---

## 📦 Context with Types

```tsx
type Theme = "light" | "dark";

const ThemeContext = React.createContext<Theme>("light");

function App() {
  const theme = React.useContext(ThemeContext);
  return <p>Theme: {theme}</p>;
}
```

---

## 🪄 Custom Hooks with Generics

```tsx
function useFetch<T>(url: string): T | null {
  const [data, setData] = React.useState<T | null>(null);

  React.useEffect(() => {
    fetch(url)
      .then((res) => res.json())
      .then(setData);
  }, [url]);

  return data;
}

// Usage
type User = { id: number; name: string };
const users = useFetch<User[]>("/api/users");
```

---

## 👶 Children Prop

```tsx
type CardProps = {
  children: React.ReactNode;
};

const Card = ({ children }: CardProps) => (
  <div className="card">{children}</div>
);

// Usage
<Card>
  <h2>Title</h2>
  <p>Content inside card</p>
</Card>
```

---

## 🛠 Utility Types (Handy for Props)

```tsx
type User = { id: number; name: string };

// Make all props optional
type PartialUser = Partial<User>;

// Require all props
type RequiredUser = Required<User>;

// Readonly props
type ReadonlyUser = Readonly<User>;

// Pick specific props
type UserName = Pick<User, "name">;

// Omit specific props
type UserWithoutId = Omit<User, "id">;
```

---
✨ **Quick Recap**

- **Props** → Define with `type` or `interface`  
- **State** → Add generic types to `useState`  
- **Refs** → Explicitly type DOM elements (`HTMLInputElement`)  
- **Events** → Use `React.ChangeEvent`, `React.FormEvent`, etc.  
- **Function Components** → `FC<Props>` or inline type annotations  
- **Context** → Pass type to `createContext<T>()`  
- **Custom Hooks** → Use generics for flexibility  
- **Children** → `React.ReactNode` for nested elements  
- **Utility Types** → `Partial`, `Pick`, `Omit`, `Readonly`, etc.  
