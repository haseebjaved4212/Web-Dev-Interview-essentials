# ⚛️ React.js Interview Essentials

> A complete, beginner-friendly reference guide covering every React concept you need to ace frontend and full-stack developer interviews. Written in simple, easy English with clear code examples and real-world patterns.

---

## 📌 Table of Contents

- [What is React?](#what-is-react)
- [How React Works (The Big Picture)](#how-react-works-the-big-picture)
- [JSX](#jsx)
- [Components](#components)
- [Props](#props)
- [State](#state)
- [useState Hook](#usestate-hook)
- [useEffect Hook](#useeffect-hook)
- [useRef Hook](#useref-hook)
- [useContext Hook](#usecontext-hook)
- [useReducer Hook](#usereducer-hook)
- [useMemo Hook](#usememo-hook)
- [useCallback Hook](#usecallback-hook)
- [Custom Hooks](#custom-hooks)
- [Component Lifecycle](#component-lifecycle)
- [Conditional Rendering](#conditional-rendering)
- [Lists and Keys](#lists-and-keys)
- [Forms and Controlled Components](#forms-and-controlled-components)
- [Event Handling](#event-handling)
- [Component Communication](#component-communication)
- [React Context API](#react-context-api)
- [React.memo](#reactmemo)
- [Code Splitting and Lazy Loading](#code-splitting-and-lazy-loading)
- [Error Boundaries](#error-boundaries)
- [Portals](#portals)
- [Refs and forwardRef](#refs-and-forwardref)
- [Higher Order Components](#higher-order-components)
- [Render Props](#render-props)
- [Compound Components](#compound-components)
- [React Router (v6)](#react-router-v6)
- [State Management Patterns](#state-management-patterns)
- [Performance Optimization](#performance-optimization)
- [Testing Basics](#testing-basics)
- [Common Interview Questions](#common-interview-questions)

---

## What is React?

React is a **JavaScript library for building user interfaces**. It was created by Facebook (now Meta) and released in 2013. React lets you break your UI into small, reusable pieces called **components**.

Think of a webpage like a car. The car has a steering wheel, seats, doors, and an engine. Each of these is a separate "component" that you build independently and put together.

Key things React gives you:

- **Component-based** — build small pieces and combine them
- **Declarative** — you tell React *what* the UI should look like, React figures out *how* to update it
- **Virtual DOM** — React keeps a lightweight copy of the DOM in memory and only updates what actually changed
- **One-way data flow** — data flows from parent to child, making it predictable and easy to debug
- **Huge ecosystem** — React Router, Redux, React Query, Next.js and thousands of other tools

---

## How React Works (The Big Picture)

When you write React, you write JavaScript that *describes* what the UI should look like. React takes that description and builds the actual HTML in the browser.

```
Your Code (JSX)
      ↓
React creates a Virtual DOM (a JavaScript object tree)
      ↓
React compares new Virtual DOM with previous one (Diffing)
      ↓
React only updates the parts of the real DOM that changed (Reconciliation)
      ↓
Browser renders the updated UI
```

This process is called **Reconciliation**. The algorithm React uses to compare Virtual DOMs is called the **Diffing Algorithm**.

### Why is this fast?

Directly updating the real DOM is slow. React batches all the changes, figures out the minimum number of updates needed, and applies them all at once. This makes React apps very fast even with lots of data changes.

---

## JSX

JSX stands for **JavaScript XML**. It looks like HTML but it is actually JavaScript under the hood. JSX lets you write your UI structure directly inside your JavaScript code.

```jsx
// This is JSX
const element = <h1 className="title">Hello, Haseeb!</h1>;

// React converts it to this behind the scenes
const element = React.createElement("h1", { className: "title" }, "Hello, Haseeb!");
```

### JSX Rules

```jsx
// 1. Always return ONE parent element (wrap in a div or Fragment)
// Wrong
return (
  <h1>Hello</h1>
  <p>World</p>   // Error: adjacent JSX elements must be wrapped
);

// Right — use a wrapper div
return (
  <div>
    <h1>Hello</h1>
    <p>World</p>
  </div>
);

// Right — use Fragment (no extra DOM node)
return (
  <>
    <h1>Hello</h1>
    <p>World</p>
  </>
);

// 2. Use className instead of class
<div className="card">...</div>

// 3. Use camelCase for HTML attributes
<input onChange={handler} />
<label htmlFor="email">Email</label>
<div style={{ backgroundColor: "red", fontSize: "16px" }}>...</div>

// 4. Self-close tags that have no children
<img src="photo.jpg" alt="photo" />
<input type="text" />
<br />

// 5. Use curly braces {} to write JavaScript inside JSX
const name = "Haseeb";
const age = 23;
return (
  <div>
    <h1>{name}</h1>
    <p>Age: {age}</p>
    <p>{age >= 18 ? "Adult" : "Minor"}</p>
    <p>{2 + 2}</p>
    <p>{"Hello".toUpperCase()}</p>
  </div>
);

// 6. Comments in JSX
return (
  <div>
    {/* This is a comment in JSX */}
    <p>Hello</p>
  </div>
);
```

---

## Components

A component is just a **JavaScript function that returns JSX**. It is like a custom HTML element that you create yourself.

```jsx
// Functional Component (modern, preferred way)
function Greeting({ name }) {
  return <h1>Hello, {name}!</h1>;
}

// Arrow function style (same thing)
const Greeting = ({ name }) => <h1>Hello, {name}!</h1>;

// Using the component
function App() {
  return (
    <div>
      <Greeting name="Haseeb" />
      <Greeting name="Ahmed" />
      <Greeting name="Sara" />
    </div>
  );
}
```

### Rules for Components

```jsx
// 1. Component name MUST start with a capital letter
function myComponent() { }  // Wrong — React treats this as an HTML tag
function MyComponent() { }  // Correct

// 2. Must return JSX (or null to render nothing)
function EmptyComponent() {
  return null;  // renders nothing
}

// 3. Components must be pure — same props = same output
// Bad (impure): modifies external variable
let count = 0;
function Counter() {
  count++;  // side effect during render — bad!
  return <p>{count}</p>;
}

// Good (pure): no side effects during render
function Counter({ value }) {
  return <p>{value}</p>;
}
```

### Component Types

```jsx
// Presentational Component (just shows UI, no logic)
function UserCard({ name, avatar, email }) {
  return (
    <div className="card">
      <img src={avatar} alt={name} />
      <h2>{name}</h2>
      <p>{email}</p>
    </div>
  );
}

// Container Component (handles logic and data, passes to children)
function UserCardContainer({ userId }) {
  const [user, setUser] = useState(null);

  useEffect(() => {
    fetchUser(userId).then(setUser);
  }, [userId]);

  if (!user) return <p>Loading...</p>;
  return <UserCard name={user.name} avatar={user.avatar} email={user.email} />;
}
```

---

## Props

Props (short for properties) are how you **pass data from a parent component to a child component**. They are like function arguments for components.

```jsx
// Parent passes props
function App() {
  return (
    <Button
      text="Click Me"
      color="blue"
      size="large"
      onClick={() => alert("Clicked!")}
      disabled={false}
    />
  );
}

// Child receives props
function Button({ text, color, size, onClick, disabled }) {
  return (
    <button
      style={{ backgroundColor: color }}
      className={`btn btn-${size}`}
      onClick={onClick}
      disabled={disabled}
    >
      {text}
    </button>
  );
}
```

### Props Deep Dive

```jsx
// Default props
function Button({ text = "Click", color = "blue", size = "medium" }) {
  return <button style={{ backgroundColor: color }}>{text}</button>;
}

// children prop (content between opening and closing tags)
function Card({ title, children }) {
  return (
    <div className="card">
      <h2>{title}</h2>
      <div className="card-body">{children}</div>
    </div>
  );
}

// Using children
function App() {
  return (
    <Card title="My Card">
      <p>This is the card content</p>
      <button>Click me</button>
    </Card>
  );
}

// Spreading props
function Input(props) {
  const { label, ...inputProps } = props;
  return (
    <div>
      <label>{label}</label>
      <input {...inputProps} />  {/* passes all remaining props to input */}
    </div>
  );
}

// Props are READ-ONLY — never modify props directly
function Child({ name }) {
  name = "Changed";  // Wrong! Never do this
  return <p>{name}</p>;
}
```

> **Key Rule:** Props flow **downward only** (parent to child). A child cannot send data up to a parent through props. For that, you pass a function as a prop.

---

## State

State is **data that belongs to a component and can change over time**. When state changes, React automatically re-renders the component to show the new data.

Think of state like a component's memory. The component "remembers" things between renders.

```
Props  = data passed FROM outside (read-only)
State  = data managed FROM inside (can change)
```

---

## useState Hook

`useState` is the most basic and commonly used hook. It lets you add state to a functional component.

```jsx
import { useState } from "react";

function Counter() {
  // [currentValue, functionToUpdateValue] = useState(initialValue)
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <button onClick={() => setCount(count - 1)}>Decrement</button>
      <button onClick={() => setCount(0)}>Reset</button>
    </div>
  );
}
```

### useState Rules and Patterns

```jsx
// 1. State can be any type: number, string, boolean, object, array
const [name, setName]       = useState("");
const [age, setAge]         = useState(0);
const [isOpen, setIsOpen]   = useState(false);
const [user, setUser]       = useState(null);
const [items, setItems]     = useState([]);
const [config, setConfig]   = useState({});

// 2. State updates are ASYNCHRONOUS — never rely on state right after setting it
const [count, setCount] = useState(0);
setCount(count + 1);
console.log(count);  // still shows OLD value!

// 3. When new state depends on old state, use the function form
// Wrong (can use stale value in async situations)
setCount(count + 1);

// Correct (always gets the latest value)
setCount(prevCount => prevCount + 1);

// 4. Never mutate state directly — always create a new copy
// Wrong: mutating array directly
const [items, setItems] = useState([1, 2, 3]);
items.push(4);        // Does NOT trigger re-render!
setItems(items);      // React sees same reference, may skip render

// Correct: create new array
setItems([...items, 4]);
setItems(prev => [...prev, 4]);

// 5. Never mutate object state directly
// Wrong
const [user, setUser] = useState({ name: "Haseeb", age: 23 });
user.name = "Ahmed"; // Does NOT trigger re-render

// Correct
setUser({ ...user, name: "Ahmed" });
setUser(prev => ({ ...prev, name: "Ahmed" }));

// 6. Lazy initialization (run expensive function only once)
// Wrong: expensiveCalc() runs on EVERY render
const [data, setData] = useState(expensiveCalc());

// Correct: only runs once on mount
const [data, setData] = useState(() => expensiveCalc());
```

### Practical useState Examples

```jsx
// Toggle
function Toggle() {
  const [isOn, setIsOn] = useState(false);
  return (
    <button onClick={() => setIsOn(prev => !prev)}>
      {isOn ? "ON" : "OFF"}
    </button>
  );
}

// Form input
function LoginForm() {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log({ email, password });
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        type="email"
        value={email}
        onChange={(e) => setEmail(e.target.value)}
        placeholder="Email"
      />
      <input
        type="password"
        value={password}
        onChange={(e) => setPassword(e.target.value)}
        placeholder="Password"
      />
      <button type="submit">Login</button>
    </form>
  );
}

// Managing a list
function TodoList() {
  const [todos, setTodos] = useState([]);
  const [input, setInput] = useState("");

  const addTodo = () => {
    if (!input.trim()) return;
    setTodos(prev => [...prev, { id: Date.now(), text: input, done: false }]);
    setInput("");
  };

  const toggleTodo = (id) => {
    setTodos(prev =>
      prev.map(todo =>
        todo.id === id ? { ...todo, done: !todo.done } : todo
      )
    );
  };

  const deleteTodo = (id) => {
    setTodos(prev => prev.filter(todo => todo.id !== id));
  };

  return (
    <div>
      <input value={input} onChange={e => setInput(e.target.value)} />
      <button onClick={addTodo}>Add</button>
      <ul>
        {todos.map(todo => (
          <li key={todo.id} style={{ textDecoration: todo.done ? "line-through" : "none" }}>
            <span onClick={() => toggleTodo(todo.id)}>{todo.text}</span>
            <button onClick={() => deleteTodo(todo.id)}>Delete</button>
          </li>
        ))}
      </ul>
    </div>
  );
}
```

---

## useEffect Hook

`useEffect` lets you **run side effects** in your component. Side effects are things that happen outside of rendering — like fetching data, setting up timers, subscribing to events, or updating the document title.

```jsx
import { useState, useEffect } from "react";

function App() {
  const [count, setCount] = useState(0);

  // Runs after EVERY render
  useEffect(() => {
    console.log("Component rendered");
  });

  // Runs ONCE on mount (empty dependency array)
  useEffect(() => {
    console.log("Component mounted");
  }, []);

  // Runs when count changes
  useEffect(() => {
    document.title = `Count: ${count}`;
  }, [count]);

  return <button onClick={() => setCount(c => c + 1)}>{count}</button>;
}
```

### Cleanup Function

```jsx
// useEffect can return a cleanup function that runs:
// - Before the effect runs again (on re-run)
// - When the component unmounts

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setSeconds(s => s + 1);
    }, 1000);

    // Cleanup: clear the interval when component unmounts
    return () => clearInterval(interval);
  }, []);  // runs once on mount

  return <p>Timer: {seconds}s</p>;
}

// Event listener cleanup
function WindowSize() {
  const [size, setSize] = useState({ width: window.innerWidth, height: window.innerHeight });

  useEffect(() => {
    const handleResize = () => {
      setSize({ width: window.innerWidth, height: window.innerHeight });
    };

    window.addEventListener("resize", handleResize);
    return () => window.removeEventListener("resize", handleResize);
  }, []);

  return <p>{size.width} x {size.height}</p>;
}
```

### Fetching Data with useEffect

```jsx
function UserProfile({ userId }) {
  const [user, setUser]     = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError]   = useState(null);

  useEffect(() => {
    // Reset state when userId changes
    setLoading(true);
    setError(null);
    setUser(null);

    let cancelled = false;  // prevent setting state on unmounted component

    async function fetchUser() {
      try {
        const res = await fetch(`/api/users/${userId}`);
        if (!res.ok) throw new Error("User not found");
        const data = await res.json();
        if (!cancelled) setUser(data);
      } catch (err) {
        if (!cancelled) setError(err.message);
      } finally {
        if (!cancelled) setLoading(false);
      }
    }

    fetchUser();

    return () => { cancelled = true; };  // cleanup on unmount or userId change
  }, [userId]);

  if (loading) return <p>Loading...</p>;
  if (error)   return <p>Error: {error}</p>;
  if (!user)   return null;

  return (
    <div>
      <h1>{user.name}</h1>
      <p>{user.email}</p>
    </div>
  );
}
```

### Dependency Array Rules

```jsx
useEffect(() => { }, );        // No array: runs after EVERY render
useEffect(() => { }, []);      // Empty array: runs ONCE on mount
useEffect(() => { }, [id]);    // Runs when id changes
useEffect(() => { }, [a, b]);  // Runs when a OR b changes

// RULE: Put everything you use inside useEffect in the dependency array
// If you use a function inside useEffect, either:
// 1. Define it inside the useEffect
// 2. Wrap it in useCallback and include it in deps
```

---

## useRef Hook

`useRef` gives you a **mutable box** that holds a value and does NOT cause a re-render when changed. It is mainly used for two things:

1. **Accessing DOM elements directly**
2. **Storing a value that survives re-renders but does not trigger re-render**

```jsx
import { useRef, useState, useEffect } from "react";

// Use Case 1: Access DOM element
function FocusInput() {
  const inputRef = useRef(null);

  const handleClick = () => {
    inputRef.current.focus();
  };

  return (
    <div>
      <input ref={inputRef} type="text" placeholder="Click button to focus" />
      <button onClick={handleClick}>Focus Input</button>
    </div>
  );
}

// Use Case 2: Store previous value (without re-rendering)
function PreviousValue() {
  const [count, setCount] = useState(0);
  const prevCountRef = useRef(0);

  useEffect(() => {
    prevCountRef.current = count;  // update AFTER render
  });

  return (
    <div>
      <p>Current: {count}</p>
      <p>Previous: {prevCountRef.current}</p>
      <button onClick={() => setCount(c => c + 1)}>Increment</button>
    </div>
  );
}

// Use Case 3: Store a timer ID (or any value that should not reset on re-render)
function Stopwatch() {
  const [time, setTime] = useState(0);
  const [running, setRunning] = useState(false);
  const intervalRef = useRef(null);

  const start = () => {
    if (running) return;
    setRunning(true);
    intervalRef.current = setInterval(() => {
      setTime(t => t + 1);
    }, 1000);
  };

  const stop = () => {
    clearInterval(intervalRef.current);
    setRunning(false);
  };

  const reset = () => {
    clearInterval(intervalRef.current);
    setRunning(false);
    setTime(0);
  };

  return (
    <div>
      <p>{time}s</p>
      <button onClick={start}>Start</button>
      <button onClick={stop}>Stop</button>
      <button onClick={reset}>Reset</button>
    </div>
  );
}
```

### useState vs useRef

| | `useState` | `useRef` |
|---|---|---|
| Causes re-render? | Yes | No |
| Value persists across renders? | Yes | Yes |
| Used for | UI data | DOM access, timers, previous values |
| How to update | `setState(newValue)` | `ref.current = newValue` |

---

## useContext Hook

`useContext` lets you **share data across many components** without passing props through every level. This is called avoiding "prop drilling".

```jsx
import { createContext, useContext, useState } from "react";

// Step 1: Create the context
const ThemeContext = createContext("light");

// Step 2: Provide the context (wrap your components)
function App() {
  const [theme, setTheme] = useState("light");

  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      <Header />
      <Main />
      <Footer />
    </ThemeContext.Provider>
  );
}

// Step 3: Consume the context anywhere in the tree
function Header() {
  const { theme, setTheme } = useContext(ThemeContext);

  return (
    <header style={{ background: theme === "dark" ? "#333" : "#fff" }}>
      <h1>My App</h1>
      <button onClick={() => setTheme(t => t === "light" ? "dark" : "light")}>
        Toggle Theme
      </button>
    </header>
  );
}

// Works at any depth — no prop drilling needed
function DeepChild() {
  const { theme } = useContext(ThemeContext);
  return <p style={{ color: theme === "dark" ? "white" : "black" }}>Deep child</p>;
}
```

### Real-World Auth Context Example

```jsx
const AuthContext = createContext(null);

export function AuthProvider({ children }) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    // Check if user is already logged in
    const savedUser = localStorage.getItem("user");
    if (savedUser) setUser(JSON.parse(savedUser));
    setLoading(false);
  }, []);

  const login = async (email, password) => {
    const data = await loginAPI(email, password);
    setUser(data.user);
    localStorage.setItem("user", JSON.stringify(data.user));
  };

  const logout = () => {
    setUser(null);
    localStorage.removeItem("user");
  };

  return (
    <AuthContext.Provider value={{ user, login, logout, loading }}>
      {children}
    </AuthContext.Provider>
  );
}

// Custom hook to use auth (best practice)
export function useAuth() {
  const context = useContext(AuthContext);
  if (!context) throw new Error("useAuth must be used within AuthProvider");
  return context;
}

// In any component
function Navbar() {
  const { user, logout } = useAuth();
  return (
    <nav>
      {user ? (
        <>
          <span>Hi, {user.name}</span>
          <button onClick={logout}>Logout</button>
        </>
      ) : (
        <a href="/login">Login</a>
      )}
    </nav>
  );
}
```

---

## useReducer Hook

`useReducer` is like `useState` but for **more complex state logic**. Instead of calling setState directly, you dispatch actions and a reducer function decides how the state changes.

Think of it like this: instead of saying "set count to 5", you say "INCREMENT" and the reducer handles how to respond.

```jsx
import { useReducer } from "react";

// 1. Define initial state
const initialState = { count: 0 };

// 2. Define reducer (pure function: old state + action → new state)
function reducer(state, action) {
  switch (action.type) {
    case "INCREMENT":
      return { count: state.count + 1 };
    case "DECREMENT":
      return { count: state.count - 1 };
    case "RESET":
      return initialState;
    case "SET":
      return { count: action.payload };
    default:
      throw new Error(`Unknown action: ${action.type}`);
  }
}

// 3. Use in component
function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: "INCREMENT" })}>+</button>
      <button onClick={() => dispatch({ type: "DECREMENT" })}>-</button>
      <button onClick={() => dispatch({ type: "RESET" })}>Reset</button>
      <button onClick={() => dispatch({ type: "SET", payload: 10 })}>Set to 10</button>
    </div>
  );
}
```

### Practical useReducer: Shopping Cart

```jsx
const cartReducer = (state, action) => {
  switch (action.type) {
    case "ADD_ITEM": {
      const exists = state.items.find(i => i.id === action.payload.id);
      if (exists) {
        return {
          ...state,
          items: state.items.map(i =>
            i.id === action.payload.id ? { ...i, qty: i.qty + 1 } : i
          )
        };
      }
      return { ...state, items: [...state.items, { ...action.payload, qty: 1 }] };
    }
    case "REMOVE_ITEM":
      return { ...state, items: state.items.filter(i => i.id !== action.payload) };
    case "CLEAR_CART":
      return { ...state, items: [] };
    default:
      return state;
  }
};

function ShoppingCart() {
  const [cart, dispatch] = useReducer(cartReducer, { items: [] });

  const total = cart.items.reduce((sum, item) => sum + item.price * item.qty, 0);

  return (
    <div>
      {cart.items.map(item => (
        <div key={item.id}>
          <span>{item.name} x{item.qty}</span>
          <button onClick={() => dispatch({ type: "REMOVE_ITEM", payload: item.id })}>
            Remove
          </button>
        </div>
      ))}
      <p>Total: ${total.toFixed(2)}</p>
      <button onClick={() => dispatch({ type: "CLEAR_CART" })}>Clear Cart</button>
    </div>
  );
}
```

### useState vs useReducer

| | `useState` | `useReducer` |
|---|---|---|
| Best for | Simple, independent values | Complex state with multiple sub-values |
| Update logic | Inline in component | Centralized in reducer |
| Testing | Harder to test logic | Reducer is a pure function, easy to test |
| Use when | 1-3 related state values | Many related values or complex transitions |

---

## useMemo Hook

`useMemo` **remembers (caches) the result of an expensive calculation** and only recalculates it when its dependencies change. This prevents doing heavy work on every single render.

```jsx
import { useState, useMemo } from "react";

// Without useMemo: runs on EVERY render (expensive!)
function ProductList({ products, searchTerm }) {
  // This runs even if only an unrelated state changes
  const filteredProducts = products.filter(p =>
    p.name.toLowerCase().includes(searchTerm.toLowerCase())
  );

  return <ul>{filteredProducts.map(p => <li key={p.id}>{p.name}</li>)}</ul>;
}

// With useMemo: only runs when products or searchTerm changes
function ProductList({ products, searchTerm }) {
  const filteredProducts = useMemo(() => {
    return products.filter(p =>
      p.name.toLowerCase().includes(searchTerm.toLowerCase())
    );
  }, [products, searchTerm]);  // only recalculate when these change

  return <ul>{filteredProducts.map(p => <li key={p.id}>{p.name}</li>)}</ul>;
}
```

```jsx
// Sorting example (heavy operation on large lists)
function SortedTable({ data, sortKey }) {
  const sortedData = useMemo(() => {
    console.log("Sorting...");
    return [...data].sort((a, b) =>
      a[sortKey] > b[sortKey] ? 1 : -1
    );
  }, [data, sortKey]);

  return (
    <table>
      {sortedData.map(row => <tr key={row.id}><td>{row[sortKey]}</td></tr>)}
    </table>
  );
}
```

> **Interview Tip:** Do NOT use `useMemo` everywhere. It has its own cost (memory + comparison). Only use it when the calculation is genuinely expensive (working with thousands of items, complex algorithms). For simple operations, the recalculation is faster than the memoization overhead.

---

## useCallback Hook

`useCallback` **remembers a function** so it does not get recreated on every render. This is useful when you pass functions as props to child components that are wrapped in `React.memo`.

```jsx
import { useState, useCallback } from "react";

// Without useCallback: new function created on every render
// This breaks React.memo because the prop reference changes every time
function Parent() {
  const [count, setCount] = useState(0);
  const [text, setText] = useState("");

  // New function on every render!
  const handleClick = () => {
    console.log("Clicked");
  };

  return (
    <div>
      <input value={text} onChange={e => setText(e.target.value)} />
      <ExpensiveChild onClick={handleClick} />
    </div>
  );
}

// With useCallback: same function reference unless deps change
function Parent() {
  const [count, setCount] = useState(0);
  const [text, setText] = useState("");

  const handleClick = useCallback(() => {
    console.log("Clicked, count:", count);
  }, [count]);  // only recreate when count changes

  return (
    <div>
      <input value={text} onChange={e => setText(e.target.value)} />
      <ExpensiveChild onClick={handleClick} />
      {/* Typing in input does not re-render ExpensiveChild now */}
    </div>
  );
}

const ExpensiveChild = React.memo(({ onClick }) => {
  console.log("ExpensiveChild rendered");
  return <button onClick={onClick}>Click Me</button>;
});
```

### useMemo vs useCallback

```jsx
// useMemo: memoizes a VALUE (result of a function)
const sortedList = useMemo(() => [...list].sort(), [list]);

// useCallback: memoizes a FUNCTION itself
const handleSort = useCallback(() => {
  setList(prev => [...prev].sort());
}, []);

// useCallback(fn, deps) is the same as:
// useMemo(() => fn, deps)
```

---

## Custom Hooks

Custom hooks are **your own reusable hooks**. They let you extract component logic into a separate function that starts with `use`. This keeps your components clean and lets you reuse logic across multiple components.

```jsx
// Custom hook: useFetch
function useFetch(url) {
  const [data, setData]       = useState(null);
  const [loading, setLoading] = useState(true);
  const [error, setError]     = useState(null);

  useEffect(() => {
    let cancelled = false;
    setLoading(true);
    setError(null);

    fetch(url)
      .then(res => {
        if (!res.ok) throw new Error(`HTTP ${res.status}`);
        return res.json();
      })
      .then(data => { if (!cancelled) setData(data); })
      .catch(err  => { if (!cancelled) setError(err.message); })
      .finally(() => { if (!cancelled) setLoading(false); });

    return () => { cancelled = true; };
  }, [url]);

  return { data, loading, error };
}

// Use it in any component — clean and simple!
function UserProfile({ id }) {
  const { data: user, loading, error } = useFetch(`/api/users/${id}`);
  if (loading) return <p>Loading...</p>;
  if (error)   return <p>Error: {error}</p>;
  return <h1>{user.name}</h1>;
}
```

### More Custom Hook Examples

```jsx
// useLocalStorage: sync state with localStorage
function useLocalStorage(key, initialValue) {
  const [value, setValue] = useState(() => {
    try {
      const item = localStorage.getItem(key);
      return item ? JSON.parse(item) : initialValue;
    } catch {
      return initialValue;
    }
  });

  const setStoredValue = (newValue) => {
    try {
      const valueToStore = newValue instanceof Function ? newValue(value) : newValue;
      setValue(valueToStore);
      localStorage.setItem(key, JSON.stringify(valueToStore));
    } catch (err) {
      console.error(err);
    }
  };

  return [value, setStoredValue];
}

// useDebounce: delay value updates
function useDebounce(value, delay) {
  const [debouncedValue, setDebouncedValue] = useState(value);

  useEffect(() => {
    const timer = setTimeout(() => setDebouncedValue(value), delay);
    return () => clearTimeout(timer);
  }, [value, delay]);

  return debouncedValue;
}

// useToggle: simple boolean toggle
function useToggle(initialValue = false) {
  const [value, setValue] = useState(initialValue);
  const toggle = useCallback(() => setValue(v => !v), []);
  return [value, toggle];
}

// Using them
function SearchBar() {
  const [query, setQuery] = useState("");
  const debouncedQuery = useDebounce(query, 300);
  const [isFiltersOpen, toggleFilters] = useToggle(false);
  const [theme, setTheme] = useLocalStorage("theme", "light");

  const { data: results } = useFetch(
    debouncedQuery ? `/api/search?q=${debouncedQuery}` : null
  );

  return (
    <div>
      <input value={query} onChange={e => setQuery(e.target.value)} />
      <button onClick={toggleFilters}>
        {isFiltersOpen ? "Hide" : "Show"} Filters
      </button>
    </div>
  );
}
```

---

## Component Lifecycle

Every React component goes through these phases:

```
Mount (component added to screen)
  → Render (JSX returned)
  → useEffect with [] runs

Update (state or props change)
  → Render again
  → useEffect with [deps] runs if deps changed

Unmount (component removed from screen)
  → useEffect cleanup functions run
```

```jsx
function LifecycleDemo({ id }) {
  const [count, setCount] = useState(0);

  // Runs ONCE when component is first added to the page
  useEffect(() => {
    console.log("Mounted!");
    return () => console.log("Unmounted!");
  }, []);

  // Runs whenever id changes
  useEffect(() => {
    console.log(`id changed to: ${id}`);
    fetchData(id);
    return () => {
      console.log("Cleaning up previous id fetch");
    };
  }, [id]);

  // Runs whenever count changes
  useEffect(() => {
    document.title = `Count: ${count}`;
  }, [count]);

  return (
    <div>
      <p>{count}</p>
      <button onClick={() => setCount(c => c + 1)}>+</button>
    </div>
  );
}
```

---

## Conditional Rendering

Showing or hiding things based on conditions is called conditional rendering.

```jsx
function Dashboard({ user, isLoading, hasError }) {

  // Method 1: if/else (good for complex conditions)
  if (isLoading) return <Spinner />;
  if (hasError)  return <ErrorMessage />;
  if (!user)     return <Login />;

  // Method 2: Ternary operator (for two options)
  return (
    <div>
      {user.isAdmin ? <AdminPanel /> : <UserPanel />}

      {/* Method 3: && (short circuit, for one optional thing) */}
      {user.notifications.length > 0 && (
        <NotificationBadge count={user.notifications.length} />
      )}

      {/* Method 4: Nullish coalescing for fallback */}
      <p>{user.bio ?? "No bio added yet"}</p>

      {/* Method 5: Variable holding JSX */}
      {(() => {
        if (user.plan === "pro") return <ProFeatures />;
        if (user.plan === "basic") return <BasicFeatures />;
        return <FreeFeatures />;
      })()}
    </div>
  );
}
```

> **Interview Tip:** Be careful with `&&`. If the left side is `0`, React renders `0` on screen (not nothing). Use `!!items.length &&` or `items.length > 0 &&` to be safe.

---

## Lists and Keys

When rendering a list of items, React needs a `key` prop on each item to track which items changed, were added, or were removed.

```jsx
function UserList({ users }) {
  return (
    <ul>
      {users.map(user => (
        // key must be unique among siblings
        <li key={user.id}>
          {user.name}
        </li>
      ))}
    </ul>
  );
}

// Wrong: using index as key (causes bugs with reordering/deletion)
{items.map((item, index) => (
  <Item key={index} data={item} />  // avoid this!
))}

// Correct: use a stable unique ID
{items.map(item => (
  <Item key={item.id} data={item} />
))}
```

### Why Keys Matter

```jsx
// Without correct keys, React can:
// - Mix up component state when reordering
// - Fail to detect item deletion correctly
// - Show wrong data in components with local state

// Correct: stable, unique IDs from your data
const products = [
  { id: "prod-1", name: "Phone" },
  { id: "prod-2", name: "Laptop" },
];

function ProductList() {
  return (
    <ul>
      {products.map(p => <li key={p.id}>{p.name}</li>)}
    </ul>
  );
}
```

---

## Forms and Controlled Components

A **controlled component** is an input whose value is controlled by React state. React is the "single source of truth" for the input's value.

```jsx
// Controlled Input (React controls the value)
function ControlledInput() {
  const [value, setValue] = useState("");

  return (
    <input
      value={value}
      onChange={e => setValue(e.target.value)}
    />
  );
}

// Full controlled form
function RegistrationForm() {
  const [form, setForm] = useState({
    name: "",
    email: "",
    password: "",
    role: "user",
    agreeToTerms: false
  });

  const [errors, setErrors] = useState({});

  // Generic change handler for all inputs
  const handleChange = (e) => {
    const { name, value, type, checked } = e.target;
    setForm(prev => ({
      ...prev,
      [name]: type === "checkbox" ? checked : value
    }));
  };

  const validate = () => {
    const newErrors = {};
    if (!form.name.trim())   newErrors.name = "Name is required";
    if (!form.email.includes("@")) newErrors.email = "Invalid email";
    if (form.password.length < 8)  newErrors.password = "Min 8 characters";
    if (!form.agreeToTerms)        newErrors.terms = "You must agree to terms";
    return newErrors;
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    const newErrors = validate();
    if (Object.keys(newErrors).length > 0) {
      setErrors(newErrors);
      return;
    }
    console.log("Form submitted:", form);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input name="name"  value={form.name}  onChange={handleChange} placeholder="Name" />
      {errors.name && <span className="error">{errors.name}</span>}

      <input name="email" value={form.email} onChange={handleChange} placeholder="Email" />
      {errors.email && <span className="error">{errors.email}</span>}

      <input name="password" type="password" value={form.password} onChange={handleChange} />
      {errors.password && <span className="error">{errors.password}</span>}

      <select name="role" value={form.role} onChange={handleChange}>
        <option value="user">User</option>
        <option value="admin">Admin</option>
      </select>

      <label>
        <input name="agreeToTerms" type="checkbox" checked={form.agreeToTerms} onChange={handleChange} />
        I agree to terms
      </label>
      {errors.terms && <span className="error">{errors.terms}</span>}

      <button type="submit">Register</button>
    </form>
  );
}
```

---

## Event Handling

```jsx
function EventExamples() {
  // Basic click handler
  const handleClick = (e) => {
    console.log("Clicked!", e.target);
    e.preventDefault();      // stop default behavior (form submit, link follow)
    e.stopPropagation();     // stop event bubbling up to parent
  };

  // Passing arguments to event handlers
  const handleDelete = (id) => {
    console.log("Delete item:", id);
  };

  // Keyboard events
  const handleKeyDown = (e) => {
    if (e.key === "Enter") console.log("Enter pressed");
    if (e.key === "Escape") console.log("Escape pressed");
    if (e.ctrlKey && e.key === "s") {
      e.preventDefault();
      console.log("Ctrl+S pressed");
    }
  };

  return (
    <div onClick={() => console.log("Div clicked")}>
      <button onClick={handleClick}>Click Me</button>

      {/* Correct way to pass arguments */}
      <button onClick={() => handleDelete(42)}>Delete #42</button>

      <input
        onKeyDown={handleKeyDown}
        onChange={e => console.log(e.target.value)}
        onFocus={() => console.log("Focused")}
        onBlur={() => console.log("Blurred")}
      />
    </div>
  );
}
```

---

## Component Communication

### Parent to Child (Props)
```jsx
function Parent() {
  return <Child message="Hello from parent" />;
}
function Child({ message }) {
  return <p>{message}</p>;
}
```

### Child to Parent (Callback Props)
```jsx
function Parent() {
  const [data, setData] = useState(null);

  const handleDataFromChild = (childData) => {
    setData(childData);
  };

  return (
    <div>
      <Child onSendData={handleDataFromChild} />
      {data && <p>Received: {data}</p>}
    </div>
  );
}

function Child({ onSendData }) {
  return (
    <button onClick={() => onSendData("Data from child!")}>
      Send to Parent
    </button>
  );
}
```

### Sibling Communication (Lift State Up)
```jsx
// When two siblings need to share state, move the state to their common parent
function Parent() {
  const [sharedValue, setSharedValue] = useState("");

  return (
    <div>
      <Input value={sharedValue} onChange={setSharedValue} />
      <Display value={sharedValue} />
    </div>
  );
}

function Input({ value, onChange }) {
  return <input value={value} onChange={e => onChange(e.target.value)} />;
}

function Display({ value }) {
  return <p>You typed: {value}</p>;
}
```

---

## React Context API

Context solves the "prop drilling" problem — passing props through many levels of components just to reach a deeply nested child.

```jsx
import { createContext, useContext, useState, useCallback } from "react";

// Create context with default value
const CartContext = createContext(null);

// Provider component
function CartProvider({ children }) {
  const [items, setItems] = useState([]);

  const addItem = useCallback((product) => {
    setItems(prev => {
      const exists = prev.find(i => i.id === product.id);
      if (exists) {
        return prev.map(i => i.id === product.id ? { ...i, qty: i.qty + 1 } : i);
      }
      return [...prev, { ...product, qty: 1 }];
    });
  }, []);

  const removeItem = useCallback((id) => {
    setItems(prev => prev.filter(i => i.id !== id));
  }, []);

  const total = items.reduce((sum, i) => sum + i.price * i.qty, 0);
  const count = items.reduce((sum, i) => sum + i.qty, 0);

  return (
    <CartContext.Provider value={{ items, addItem, removeItem, total, count }}>
      {children}
    </CartContext.Provider>
  );
}

// Custom hook
function useCart() {
  const ctx = useContext(CartContext);
  if (!ctx) throw new Error("useCart must be used within CartProvider");
  return ctx;
}

// Wrap app
function App() {
  return (
    <CartProvider>
      <Navbar />
      <ProductGrid />
    </CartProvider>
  );
}

// Use anywhere
function Navbar() {
  const { count } = useCart();
  return <nav>Cart ({count})</nav>;
}

function ProductCard({ product }) {
  const { addItem } = useCart();
  return (
    <div>
      <p>{product.name} - ${product.price}</p>
      <button onClick={() => addItem(product)}>Add to Cart</button>
    </div>
  );
}
```

---

## React.memo

`React.memo` wraps a component and **prevents it from re-rendering if its props have not changed**.

```jsx
import { memo, useState } from "react";

// Without memo: re-renders even when count changes but not name
function ExpensiveComponent({ name }) {
  console.log("ExpensiveComponent rendered!");
  return <div>Hello, {name}</div>;
}

// With memo: only re-renders when name actually changes
const ExpensiveComponent = memo(function ExpensiveComponent({ name }) {
  console.log("ExpensiveComponent rendered!");
  return <div>Hello, {name}</div>;
});

function App() {
  const [count, setCount] = useState(0);
  const [name, setName] = useState("Haseeb");

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(c => c + 1)}>Increment Count</button>
      {/* Clicking the button above does NOT re-render ExpensiveComponent */}
      <ExpensiveComponent name={name} />
    </div>
  );
}

// Custom comparison function (for complex props)
const UserCard = memo(({ user }) => {
  return <div>{user.name}</div>;
}, (prevProps, nextProps) => {
  // Return true if props are equal (skip re-render)
  // Return false if props changed (do re-render)
  return prevProps.user.id === nextProps.user.id &&
         prevProps.user.name === nextProps.user.name;
});
```

---

## Code Splitting and Lazy Loading

Load parts of your app only when they are needed. This makes the initial page load much faster.

```jsx
import { lazy, Suspense } from "react";

// Instead of: import Dashboard from "./Dashboard";
// Use lazy import — loads only when needed
const Dashboard = lazy(() => import("./Dashboard"));
const UserProfile = lazy(() => import("./UserProfile"));
const AdminPanel = lazy(() => import("./AdminPanel"));

function App() {
  return (
    // Suspense shows fallback while the component loads
    <Suspense fallback={<div>Loading page...</div>}>
      <Router>
        <Routes>
          <Route path="/"         element={<Home />} />
          <Route path="/dashboard" element={<Dashboard />} />
          <Route path="/profile"  element={<UserProfile />} />
          <Route path="/admin"    element={<AdminPanel />} />
        </Routes>
      </Router>
    </Suspense>
  );
}

// Custom loading UI
const PageLoader = () => (
  <div style={{ display: "flex", justifyContent: "center", padding: "100px" }}>
    <Spinner />
  </div>
);

<Suspense fallback={<PageLoader />}>
  <Dashboard />
</Suspense>
```

---

## Error Boundaries

Error boundaries **catch JavaScript errors anywhere in their child component tree** and show a fallback UI instead of crashing the whole app. They must be class components (hooks do not support this yet).

```jsx
import { Component } from "react";

class ErrorBoundary extends Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false, error: null };
  }

  // Called when a child throws an error
  static getDerivedStateFromError(error) {
    return { hasError: true, error };
  }

  // Called after error is caught (good for logging)
  componentDidCatch(error, info) {
    console.error("Error caught:", error);
    console.error("Component stack:", info.componentStack);
    // logErrorToService(error, info);
  }

  render() {
    if (this.state.hasError) {
      return this.props.fallback || (
        <div>
          <h2>Something went wrong!</h2>
          <button onClick={() => this.setState({ hasError: false, error: null })}>
            Try Again
          </button>
        </div>
      );
    }
    return this.props.children;
  }
}

// Use it to wrap parts of your app
function App() {
  return (
    <ErrorBoundary fallback={<p>Failed to load header</p>}>
      <Header />
    </ErrorBoundary>
    <ErrorBoundary fallback={<p>Failed to load dashboard</p>}>
      <Dashboard />
    </ErrorBoundary>
  );
}
```

---

## Portals

Portals let you **render a component outside of its parent's DOM node**. This is perfect for modals, tooltips, and dropdowns that need to be at the top of the DOM to avoid clipping or z-index issues.

```jsx
import { createPortal } from "react-dom";

function Modal({ isOpen, onClose, children }) {
  if (!isOpen) return null;

  // Renders into document.body, NOT inside the parent div
  return createPortal(
    <div className="modal-overlay" onClick={onClose}>
      <div className="modal-content" onClick={e => e.stopPropagation()}>
        <button className="modal-close" onClick={onClose}>✕</button>
        {children}
      </div>
    </div>,
    document.body  // portal target
  );
}

function App() {
  const [isOpen, setIsOpen] = useState(false);

  return (
    <div style={{ overflow: "hidden" }}>
      {/* overflow: hidden won't clip the modal because it renders in body */}
      <button onClick={() => setIsOpen(true)}>Open Modal</button>
      <Modal isOpen={isOpen} onClose={() => setIsOpen(false)}>
        <h2>Modal Title</h2>
        <p>Modal content here</p>
      </Modal>
    </div>
  );
}
```

---

## Refs and forwardRef

`forwardRef` lets a parent component **access a DOM element inside a child component** through a ref.

```jsx
import { forwardRef, useRef } from "react";

// Regular component — parent cannot access its input DOM node
function Input({ label, ...props }) {
  return (
    <div>
      <label>{label}</label>
      <input {...props} />
    </div>
  );
}

// With forwardRef — parent CAN access the input DOM node
const Input = forwardRef(function Input({ label, ...props }, ref) {
  return (
    <div>
      <label>{label}</label>
      <input ref={ref} {...props} />
    </div>
  );
});

// Parent uses it
function LoginForm() {
  const emailRef = useRef(null);
  const passwordRef = useRef(null);

  const focusEmail = () => emailRef.current.focus();

  return (
    <form>
      <Input ref={emailRef}    label="Email"    type="email" />
      <Input ref={passwordRef} label="Password" type="password" />
      <button type="button" onClick={focusEmail}>Focus Email</button>
    </form>
  );
}
```

---

## Higher Order Components

A Higher Order Component (HOC) is a **function that takes a component and returns a new, enhanced component**. It is a pattern for reusing component logic.

```jsx
// HOC: adds loading state
function withLoading(WrappedComponent) {
  return function WithLoadingComponent({ isLoading, ...props }) {
    if (isLoading) return <div>Loading...</div>;
    return <WrappedComponent {...props} />;
  };
}

// HOC: adds authentication check
function withAuth(WrappedComponent) {
  return function WithAuthComponent(props) {
    const { user } = useAuth();
    if (!user) return <Navigate to="/login" />;
    return <WrappedComponent {...props} />;
  };
}

// HOC: adds error boundary
function withErrorBoundary(WrappedComponent, fallback) {
  return function WithErrorBoundaryComponent(props) {
    return (
      <ErrorBoundary fallback={fallback}>
        <WrappedComponent {...props} />
      </ErrorBoundary>
    );
  };
}

// Usage
const UserListWithLoading = withLoading(UserList);
const ProtectedDashboard  = withAuth(Dashboard);
const SafeWidget          = withErrorBoundary(Widget, <p>Widget failed</p>);

// Apply multiple HOCs
const Component = withAuth(withLoading(withErrorBoundary(Dashboard)));

// Or compose them
const enhance = (Component) =>
  withAuth(withLoading(withErrorBoundary(Component)));
const EnhancedDashboard = enhance(Dashboard);
```

---

## Render Props

Render Props is a pattern where a component receives a **function as a prop** and uses that function to decide what to render. It is another way to share logic between components.

```jsx
// Component with render prop
function MouseTracker({ render }) {
  const [position, setPosition] = useState({ x: 0, y: 0 });

  return (
    <div
      style={{ height: "300px", border: "1px solid" }}
      onMouseMove={e => setPosition({ x: e.clientX, y: e.clientY })}
    >
      {render(position)}  {/* call the function with the data */}
    </div>
  );
}

// Use it — pass different UIs without changing MouseTracker
function App() {
  return (
    <div>
      <MouseTracker render={({ x, y }) => (
        <p>Mouse is at {x}, {y}</p>
      )} />

      <MouseTracker render={({ x, y }) => (
        <div style={{ position: "absolute", left: x, top: y }}>
          🐭
        </div>
      )} />
    </div>
  );
}

// The "children as a function" variation
function DataProvider({ children, url }) {
  const { data, loading } = useFetch(url);
  return children({ data, loading });
}

<DataProvider url="/api/users">
  {({ data, loading }) => loading ? <Spinner /> : <UserList users={data} />}
</DataProvider>
```

---

## Compound Components

Compound components are a **group of components that work together** and share implicit state through context. Think of how `<select>` and `<option>` work together.

```jsx
import { createContext, useContext, useState } from "react";

const TabsContext = createContext(null);

// Parent component manages shared state
function Tabs({ children, defaultTab }) {
  const [activeTab, setActiveTab] = useState(defaultTab);

  return (
    <TabsContext.Provider value={{ activeTab, setActiveTab }}>
      <div className="tabs">{children}</div>
    </TabsContext.Provider>
  );
}

// Child components access shared state via context
function TabList({ children }) {
  return <div className="tab-list">{children}</div>;
}

function Tab({ id, children }) {
  const { activeTab, setActiveTab } = useContext(TabsContext);
  return (
    <button
      className={`tab ${activeTab === id ? "active" : ""}`}
      onClick={() => setActiveTab(id)}
    >
      {children}
    </button>
  );
}

function TabPanels({ children }) {
  return <div className="tab-panels">{children}</div>;
}

function TabPanel({ id, children }) {
  const { activeTab } = useContext(TabsContext);
  if (activeTab !== id) return null;
  return <div className="tab-panel">{children}</div>;
}

// Attach sub-components to parent
Tabs.List   = TabList;
Tabs.Tab    = Tab;
Tabs.Panels = TabPanels;
Tabs.Panel  = TabPanel;

// Clean, readable usage
function App() {
  return (
    <Tabs defaultTab="profile">
      <Tabs.List>
        <Tabs.Tab id="profile">Profile</Tabs.Tab>
        <Tabs.Tab id="settings">Settings</Tabs.Tab>
        <Tabs.Tab id="billing">Billing</Tabs.Tab>
      </Tabs.List>
      <Tabs.Panels>
        <Tabs.Panel id="profile"><ProfilePanel /></Tabs.Panel>
        <Tabs.Panel id="settings"><SettingsPanel /></Tabs.Panel>
        <Tabs.Panel id="billing"><BillingPanel /></Tabs.Panel>
      </Tabs.Panels>
    </Tabs>
  );
}
```

---

## React Router (v6)

React Router lets you build **multi-page navigation** in a single page app (SPA).

```jsx
import { BrowserRouter, Routes, Route, Link, NavLink,
         useNavigate, useParams, useLocation, Navigate, Outlet } from "react-router-dom";

// Setup
function App() {
  return (
    <BrowserRouter>
      <Navbar />
      <Routes>
        <Route path="/"            element={<Home />} />
        <Route path="/about"       element={<About />} />
        <Route path="/users"       element={<Users />} />
        <Route path="/users/:id"   element={<UserDetail />} />
        <Route path="/dashboard"   element={<ProtectedRoute><Dashboard /></ProtectedRoute>} />
        <Route path="*"            element={<NotFound />} />
      </Routes>
    </BrowserRouter>
  );
}

// Navigation
function Navbar() {
  return (
    <nav>
      <Link to="/">Home</Link>

      {/* NavLink adds "active" class when route matches */}
      <NavLink to="/about" className={({ isActive }) => isActive ? "active" : ""}>
        About
      </NavLink>
    </nav>
  );
}

// URL Params
function UserDetail() {
  const { id } = useParams();
  const { data: user } = useFetch(`/api/users/${id}`);
  return <h1>{user?.name}</h1>;
}

// Programmatic navigation
function LoginPage() {
  const navigate = useNavigate();

  const handleLogin = async () => {
    await login();
    navigate("/dashboard");           // go to route
    navigate(-1);                     // go back one page
    navigate("/dashboard", { replace: true });  // replace history entry
  };

  return <button onClick={handleLogin}>Login</button>;
}

// Location (current URL info)
function Page() {
  const location = useLocation();
  console.log(location.pathname);   // "/users"
  console.log(location.search);     // "?tab=profile"
  console.log(location.state);      // state passed with navigate()
}

// Nested Routes
function Dashboard() {
  return (
    <div>
      <DashboardNav />
      <Outlet />  {/* renders the matched child route */}
    </div>
  );
}

// Protected Route
function ProtectedRoute({ children }) {
  const { user } = useAuth();
  if (!user) return <Navigate to="/login" replace />;
  return children;
}
```

---

## State Management Patterns

### Local State (useState / useReducer)
Best for component-specific data like form values, toggles, loading states.

### Lifted State
When siblings need to share state, move it up to the nearest common parent.

### Context API
Good for global data like theme, auth, language. Not ideal for frequently changing data (causes many re-renders).

### Zustand (lightweight, popular alternative to Redux)

```jsx
import { create } from "zustand";

const useStore = create((set) => ({
  count: 0,
  user: null,
  increment: () => set(state => ({ count: state.count + 1 })),
  decrement: () => set(state => ({ count: state.count - 1 })),
  setUser: (user) => set({ user }),
  reset: () => set({ count: 0, user: null })
}));

// Use in any component — no Provider needed!
function Counter() {
  const { count, increment, decrement } = useStore();
  return (
    <div>
      <p>{count}</p>
      <button onClick={increment}>+</button>
      <button onClick={decrement}>-</button>
    </div>
  );
}

function Navbar() {
  const user = useStore(state => state.user);  // select only what you need
  return <nav>{user?.name}</nav>;
}
```

### React Query (for server state / data fetching)

```jsx
import { useQuery, useMutation, useQueryClient } from "@tanstack/react-query";

function Users() {
  // Automatic caching, loading, error states, refetching
  const { data: users, isLoading, error } = useQuery({
    queryKey: ["users"],
    queryFn: () => fetch("/api/users").then(r => r.json()),
    staleTime: 5 * 60 * 1000  // data fresh for 5 minutes
  });

  const queryClient = useQueryClient();

  const { mutate: deleteUser } = useMutation({
    mutationFn: (id) => fetch(`/api/users/${id}`, { method: "DELETE" }),
    onSuccess: () => {
      queryClient.invalidateQueries({ queryKey: ["users"] });
    }
  });

  if (isLoading) return <Spinner />;
  if (error)     return <p>Error: {error.message}</p>;

  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>
          {user.name}
          <button onClick={() => deleteUser(user.id)}>Delete</button>
        </li>
      ))}
    </ul>
  );
}
```

---

## Performance Optimization

```jsx
// 1. React.memo — prevent re-render when props don't change
const UserCard = memo(({ user }) => <div>{user.name}</div>);

// 2. useCallback — stable function references
const handleClick = useCallback(() => doSomething(id), [id]);

// 3. useMemo — cache expensive calculations
const sorted = useMemo(() => [...data].sort(compareFn), [data]);

// 4. Lazy loading — load components only when needed
const Chart = lazy(() => import("./Chart"));

// 5. Virtualization — only render visible items (for huge lists)
// Use react-window or react-virtual
import { FixedSizeList } from "react-window";

function BigList({ items }) {
  return (
    <FixedSizeList
      height={600}
      width="100%"
      itemCount={items.length}
      itemSize={50}
    >
      {({ index, style }) => (
        <div style={style}>{items[index].name}</div>
      )}
    </FixedSizeList>
  );
}

// 6. Key prop on list items — helps React reconcile faster

// 7. Avoid anonymous functions inline where possible for memoized children
// Bad: new function every render
<Button onClick={() => handleClick(id)} />

// Good with useCallback:
const handleItemClick = useCallback(() => handleClick(id), [id]);
<Button onClick={handleItemClick} />

// 8. Batch state updates (React 18 does this automatically)
// React 18: these two updates cause only ONE re-render
setCount(c => c + 1);
setName("Haseeb");

// 9. useTransition (React 18) — mark non-urgent updates
import { useTransition } from "react";

function SearchResults() {
  const [query, setQuery] = useState("");
  const [results, setResults] = useState([]);
  const [isPending, startTransition] = useTransition();

  const handleSearch = (e) => {
    setQuery(e.target.value);  // urgent: update input immediately

    startTransition(() => {
      // Non-urgent: filtering can wait, keep UI responsive
      setResults(filterItems(e.target.value));
    });
  };

  return (
    <div>
      <input onChange={handleSearch} value={query} />
      {isPending ? <p>Filtering...</p> : <ResultsList results={results} />}
    </div>
  );
}
```

---

## Testing Basics

```jsx
// React Testing Library (most popular approach)
import { render, screen, fireEvent, waitFor } from "@testing-library/react";
import userEvent from "@testing-library/user-event";

// Test 1: Component renders correctly
test("renders greeting", () => {
  render(<Greeting name="Haseeb" />);
  expect(screen.getByText("Hello, Haseeb!")).toBeInTheDocument();
});

// Test 2: Button click updates state
test("counter increments on click", async () => {
  const user = userEvent.setup();
  render(<Counter />);

  const button = screen.getByRole("button", { name: /increment/i });
  await user.click(button);

  expect(screen.getByText("Count: 1")).toBeInTheDocument();
});

// Test 3: Form submission
test("login form submits with correct data", async () => {
  const user = userEvent.setup();
  const handleSubmit = jest.fn();
  render(<LoginForm onSubmit={handleSubmit} />);

  await user.type(screen.getByLabelText(/email/i), "test@example.com");
  await user.type(screen.getByLabelText(/password/i), "password123");
  await user.click(screen.getByRole("button", { name: /login/i }));

  expect(handleSubmit).toHaveBeenCalledWith({
    email: "test@example.com",
    password: "password123"
  });
});

// Test 4: Async data fetching
test("loads and displays users", async () => {
  global.fetch = jest.fn().mockResolvedValue({
    ok: true,
    json: () => Promise.resolve([{ id: 1, name: "Haseeb" }])
  });

  render(<UserList />);

  expect(screen.getByText("Loading...")).toBeInTheDocument();

  await waitFor(() => {
    expect(screen.getByText("Haseeb")).toBeInTheDocument();
  });
});
```

---

## Common Interview Questions

### Q1. What is React and why would you use it?
React is a JavaScript library for building user interfaces using reusable components. You would use it because it makes complex UIs easy to build and maintain, updates the DOM efficiently via the Virtual DOM, has a huge ecosystem, and makes it easy to share logic across your app using hooks.

### Q2. What is the Virtual DOM and how does it work?
The Virtual DOM is a lightweight JavaScript copy of the real DOM that React keeps in memory. When state changes, React creates a new Virtual DOM, compares it with the previous one (diffing), finds exactly what changed, and updates only those parts in the real DOM. This is much faster than updating the whole real DOM every time.

### Q3. What are the rules of hooks?
There are two main rules. First, only call hooks at the top level of your component — never inside loops, conditions, or nested functions. Second, only call hooks from React function components or other custom hooks — never from regular JavaScript functions. These rules exist because React tracks hooks by their call order.

### Q4. What is the difference between state and props?
Props are data passed into a component from outside (read-only, the child cannot change them). State is data that lives inside a component and can change over time (managed by the component itself). When either changes, the component re-renders.

### Q5. When would you use useReducer instead of useState?
Use `useReducer` when your state is complex (an object with many fields), when multiple state values are closely related, when the next state depends on the previous in complex ways, or when you need to keep your update logic centralized and easy to test (since the reducer is a pure function).

### Q6. What is prop drilling and how do you solve it?
Prop drilling is when you pass props through many layers of components just to get data to a deeply nested child, even though the middle components do not need that data. You solve it with Context API (for global, rarely-changing data) or a state management library like Zustand or Redux (for frequently changing shared data).

### Q7. What is the difference between useMemo and useCallback?
`useMemo` caches the **result** of a function (a computed value). `useCallback` caches the **function itself**. Use `useMemo` when you want to avoid recalculating an expensive value. Use `useCallback` when you want to give a stable function reference to a memoized child component so it does not re-render unnecessarily.

### Q8. Why do we need keys in lists?
Keys help React identify which items in a list have changed, been added, or been removed. Without keys (or with bad keys like array indexes), React may re-render the wrong components, mix up local state in list items, or perform unnecessary DOM operations. Always use a stable, unique ID from your data.

### Q9. What is React.memo and when should you use it?
`React.memo` is a higher-order component that wraps a functional component and prevents it from re-rendering if its props have not changed. Use it when a child component renders often but its props rarely change, and the re-render is causing performance issues. Do not use it everywhere — the memoization itself has a small cost.

### Q10. What are controlled vs uncontrolled components?
A controlled component is an input whose value is controlled by React state — React is the source of truth. An uncontrolled component stores its own value in the DOM and you access it with a ref. Controlled components are the React way because they make the value predictable and easy to validate or transform.

### Q11. What is the useEffect dependency array?
The dependency array tells React when to run the effect. An empty array `[]` means run once on mount. An array with values like `[userId]` means run whenever `userId` changes. No array at all means run after every render. You should include every value from the component that the effect uses in the dependency array.

### Q12. What happens when you call setState inside useEffect?
It depends on the dependencies. If the state you set is in the dependency array, you will create an infinite loop (state changes → effect runs → state changes again). Make sure state updates inside useEffect are conditional or only triggered by external events, not by the state itself.

### Q13. What is the difference between useEffect and useLayoutEffect?
`useEffect` runs asynchronously after the browser has painted the screen (non-blocking). `useLayoutEffect` runs synchronously after DOM updates but before the browser paints. Use `useLayoutEffect` only when you need to read or modify the DOM layout before the user sees it (like measuring element dimensions or preventing flash). For most things, use `useEffect`.

### Q14. How does React handle re-renders?
A component re-renders when its state changes, when its props change, when its parent re-renders (even if props did not change), or when a context it subscribes to changes. React batches multiple state updates together in React 18 to minimize re-renders. You can prevent unnecessary re-renders with `React.memo`, `useMemo`, and `useCallback`.

### Q15. What are the main differences between React 17 and React 18?
React 18 introduced automatic batching (multiple state updates in async operations now batch into one re-render), the `useTransition` and `useDeferredValue` hooks for marking non-urgent updates, the new `createRoot` API for rendering, Suspense improvements, and the foundation for concurrent features that let React pause and resume rendering work.

---

## Contributing

Found a mistake or want to add something? Open a PR or raise an issue. All contributions are welcome.

---

## Author

**Haseeb Javed**
Full-Stack Developer | React, Django, FastAPI

- GitHub: [@haseebjaved4212](https://github.com/haseebjaved4212)
- Email: contactimhaseeb@gmail.com

---

## License

This project is open source and available under the [MIT License](LICENSE).