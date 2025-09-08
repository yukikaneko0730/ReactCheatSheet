# 🎨 React UI Snippets

This section contains **commonly used UI code snippets** in React.  
Perfect for building buttons, cards, modals, forms, and more. 🚀

---

## 🔘 Button

A simple reusable button with styling.

```jsx
const Button = ({ label, onClick }) => (
  <button
    onClick={onClick}
    className="px-4 py-2 bg-blue-500 text-white rounded hover:bg-blue-600"
  >
    {label}
  </button>
);

// Usage
<Button label="Click me" onClick={() => alert("Pressed!")} />

---

## 📦 Card (Box)

A card layout for displaying content.

```jsx
const Card = ({ title, content }) => (
  <div className="border p-4 rounded shadow-md bg-white">
    <h2 className="font-bold text-lg">{title}</h2>
    <p>{content}</p>
  </div>
);

// Usage
<Card title="Notice" content="Today’s weather is sunny ☀️" />
```

---

## 🪟 Modal

A simple modal component with overlay.

```jsx
const Modal = ({ isOpen, onClose, children }) => {
  if (!isOpen) return null;
  return (
    <div className="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center">
      <div className="bg-white p-6 rounded shadow-lg">
        {children}
        <button onClick={onClose} className="mt-4 text-blue-500">Close</button>
      </div>
    </div>
  );
};

// Usage
const App = () => {
  const [open, setOpen] = React.useState(false);
  return (
    <>
      <button onClick={() => setOpen(true)}>Open Modal</button>
      <Modal isOpen={open} onClose={() => setOpen(false)}>
        <h2>Hello Modal!</h2>
      </Modal>
    </>
  );
};
```

---

## 📋 Form

Basic form with controlled input.

´´´jsx
const Form = () => {
  const [text, setText] = React.useState("");

  const handleSubmit = (e) => {
    e.preventDefault();
    alert(`Submitted: ${text}`);
  };

  return (
    <form onSubmit={handleSubmit} className="space-y-2">
      <input
        type="text"
        value={text}
        onChange={(e) => setText(e.target.value)}
        className="border p-2 w-full rounded"
      />
      <button className="px-4 py-2 bg-green-500 text-white rounded">
        Submit
      </button>
    </form>
  );
};
```

---

## 📑 Tabs

Switch between sections with simple tabs.

```jsx
const Tabs = () => {
  const [active, setActive] = React.useState("A");

  return (
    <div>
      <div className="flex gap-4 border-b">
        {["A", "B", "C"].map((tab) => (
          <button
            key={tab}
            onClick={() => setActive(tab)}
            className={active === tab ? "border-b-2 border-blue-500" : ""}
          >
            {tab}
          </button>
        ))}
      </div>
      <div className="p-4">Content of Tab {active}</div>
    </div>
  );
};
```

---

## 📅 Calendar (with react-calendar)

```bash

npm install react-calendar

```

```jsx
import { useState } from "react";
import Calendar from "react-calendar";
import "react-calendar/dist/Calendar.css";

const CalendarExample = () => {
  const [date, setDate] = useState(new Date());
  return <Calendar onChange={setDate} value={date} />;
};
```

---

## 📜 Table

Useful for displaying structured data.

```jsx
const Table = ({ data }) => (
  <table className="border-collapse border border-gray-400 w-full">
    <thead>
      <tr>
        <th className="border p-2">Name</th>
        <th className="border p-2">Age</th>
      </tr>
    </thead>
    <tbody>
      {data.map((row, i) => (
        <tr key={i}>
          <td className="border p-2">{row.name}</td>
          <td className="border p-2">{row.age}</td>
        </tr>
      ))}
    </tbody>
  </table>
);

// Usage
<Table data={[{ name: "Alice", age: 25 }, { name: "Bob", age: 30 }]} />
```

---

## 📌 Tooltip

Show extra info on hover.

```jsx
const Tooltip = ({ text, children }) => (
  <span className="relative group cursor-pointer">
    {children}
    <span className="absolute bottom-full mb-2 hidden group-hover:block bg-black text-white text-xs p-1 rounded">
      {text}
    </span>
  </span>
);

// Usage
<Tooltip text="More info here">
  <button>Hover me</button>
</Tooltip>
```

---

## 🗺️ Navbar

A common navigation bar.

```jsx
const Navbar = () => (
  <nav className="flex gap-4 bg-gray-100 p-4">
    <a href="/">Home</a>
    <a href="/about">About</a>
    <a href="/contact">Contact</a>
  </nav>
);
```

---

## 📥 Dropdown Menu

Select from a list of options.

```jsx
const Dropdown = ({ options, onSelect }) => (
  <select onChange={(e) => onSelect(e.target.value)} className="border p-2 rounded">
    {options.map((opt, i) => (
      <option key={i} value={opt}>{opt}</option>
    ))}
  </select>
);

// Usage
<Dropdown options={["Option A", "Option B", "Option C"]} onSelect={(val) => alert(val)} />
```

---

## 🌙 Toggle (Switch)

For settings or dark mode toggles.

```jsx
const Toggle = () => {
  const [on, setOn] = React.useState(false);
  return (
    <button
      onClick={() => setOn(!on)}
      className={`px-4 py-2 rounded ${on ? "bg-green-500" : "bg-gray-400"}`}
    >
      {on ? "ON" : "OFF"}
    </button>
  );
};
```

---

## 🔔 Notification (Toast)

Show temporary messages.

```jsx
const Toast = ({ message }) => (
  <div className="fixed bottom-4 right-4 bg-black text-white px-4 py-2 rounded shadow">
    {message}
  </div>
);

// Usage
<Toast message="Saved successfully ✅" />
````

---

✨ **Quick Recap**

- **Button** → Reusable action triggers  
- **Card** → Display structured content  
- **Modal** → Overlay for dialogs  
- **Form** → Controlled input with submit  
- **Tabs** → Switch between sections  
- **Calendar** → Pick and display dates  
- **Chart** → Visualize data with `recharts`  
- **Table** → Display tabular data  
- **Tooltip** → Show info on hover  
- **Navbar** → Navigation links  
- **Dropdown** → Select options  
- **Toggle** → On/Off switch  
- **Toast** → Temporary notification  




