# 16. All code samples

[Back to notes index](../README.md)

| [Previous: Accessibility, transitions, and performance](15-accessibility-transitions-and-performance.md) | [Notes index](../README.md) | [Next: Complete questions and answers](99-complete-q-and-a.md) |
|:--|:--:|--:|

## 1. React foundations and project setup

~~~sh
npm create vite@latest hello-react -- --template react
cd hello-react
npm install
npm run dev
~~~

~~~html
<div id="root"></div>
~~~

~~~jsx
import { createRoot } from "react-dom/client";
import App from "./App.jsx";

const rootElement = document.getElementById("root");

if (!rootElement) {
  throw new Error("The root element is missing.");
}

createRoot(rootElement).render(<App />);
~~~

~~~jsx
export default function App() {
  return (
    <main>
      <h1>My first React screen</h1>
      <p>This page is rendered from a JavaScript component.</p>
    </main>
  );
}
~~~

## 2. JSX and rendering

~~~jsx
function Welcome({ name, unreadCount }) {
  return (
    <section className="welcome">
      <h1>Hello, {name}</h1>
      <p>
        {unreadCount === 0
          ? "You are all caught up."
          : "You have " + unreadCount + " unread messages."}
      </p>
      <label htmlFor="search">Search</label>
      <input id="search" name="search" />
    </section>
  );
}
~~~

~~~jsx
function SaveButton() {
  function handleSave() {
    console.log("Saved");
  }

  return <button onClick={handleSave}>Save</button>;
}
~~~

## 3. Components, props, and composition

~~~jsx
function ProfileCard({ person, onOpen }) {
  return (
    <article className="profile-card">
      <h2>{person.name}</h2>
      <p>{person.role}</p>
      <button onClick={() => onOpen(person.id)}>View profile</button>
    </article>
  );
}

function Team({ people }) {
  function openProfile(id) {
    console.log("Open profile:", id);
  }

  return (
    <section>
      {people.map((person) => (
        <ProfileCard
          key={person.id}
          person={person}
          onOpen={openProfile}
        />
      ))}
    </section>
  );
}
~~~

~~~jsx
function Panel({ title, children }) {
  return (
    <section className="panel">
      <h2>{title}</h2>
      <div>{children}</div>
    </section>
  );
}

function Summary() {
  return (
    <Panel title="Today">
      <p>Three tasks are complete.</p>
    </Panel>
  );
}
~~~

## 4. State and events

~~~jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  function addOne() {
    setCount((currentCount) => currentCount + 1);
  }

  return (
    <section>
      <p>Count: {count}</p>
      <button onClick={addOne}>Add one</button>
    </section>
  );
}
~~~

~~~jsx
setProfile((current) => ({
  ...current,
  city: "Bengaluru",
}));

setTasks((current) =>
  current.map((task) =>
    task.id === targetId ? { ...task, done: true } : task
  )
);
~~~

## 5. Conditional rendering, lists, and keys

~~~jsx
function Notice({ loading, error, message }) {
  if (loading) {
    return <p role="status">Loading message...</p>;
  }

  if (error) {
    return <p role="alert">{error}</p>;
  }

  return <p>{message || "No message yet."}</p>;
}
~~~

~~~jsx
{isAdmin && <a href="/settings">Settings</a>}
~~~

~~~jsx
const tasks = [
  { id: "t-1", label: "Read notes", done: true },
  { id: "t-2", label: "Practice state updates", done: false },
];

function TaskList() {
  return (
    <ul>
      {tasks.map((task) => (
        <li key={task.id}>
          <span>{task.label}</span>
          {task.done ? " (complete)" : " (open)"}
        </li>
      ))}
    </ul>
  );
}
~~~

## 6. Forms and validation

~~~jsx
import { useState } from "react";

function ContactForm() {
  const [email, setEmail] = useState("");
  const [message, setMessage] = useState("");

  function handleSubmit(event) {
    event.preventDefault();

    if (!email.includes("@")) {
      setMessage("Enter a valid email address.");
      return;
    }

    setMessage("Your contact details are ready to send.");
  }

  return (
    <form onSubmit={handleSubmit}>
      <label htmlFor="email">Email address</label>
      <input
        id="email"
        name="email"
        type="email"
        value={email}
        onChange={(event) => setEmail(event.target.value)}
        aria-describedby="email-help"
        required
      />
      <p id="email-help">Use an address where you can be reached.</p>
      <button type="submit">Continue</button>
      {message && <p role="status">{message}</p>}
    </form>
  );
}
~~~

## 7. State design and lifting state

~~~jsx
function ProductSearch({ products }) {
  const [query, setQuery] = useState("");
  const normalizedQuery = query.trim().toLowerCase();

  const visibleProducts = products.filter((product) =>
    product.name.toLowerCase().includes(normalizedQuery)
  );

  return (
    <section>
      <label htmlFor="product-search">Search products</label>
      <input
        id="product-search"
        value={query}
        onChange={(event) => setQuery(event.target.value)}
      />
      <p>{visibleProducts.length} products found</p>
      <ul>
        {visibleProducts.map((product) => (
          <li key={product.id}>{product.name}</li>
        ))}
      </ul>
    </section>
  );
}
~~~

## 8. Reducers and context

~~~jsx
import { useReducer } from "react";

const initialState = { count: 0 };

function counterReducer(state, action) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    case "decrement":
      return { count: state.count - 1 };
    case "reset":
      return initialState;
    default:
      throw new Error("Unknown counter action.");
  }
}

function Counter() {
  const [state, dispatch] = useReducer(counterReducer, initialState);

  return (
    <section>
      <p>{state.count}</p>
      <button onClick={() => dispatch({ type: "decrement" })}>Down</button>
      <button onClick={() => dispatch({ type: "increment" })}>Up</button>
      <button onClick={() => dispatch({ type: "reset" })}>Reset</button>
    </section>
  );
}
~~~

## 9. Effects and external systems

~~~jsx
import { useEffect, useState } from "react";

function OnlineStatus() {
  const [online, setOnline] = useState(navigator.onLine);

  useEffect(() => {
    function updateStatus() {
      setOnline(navigator.onLine);
    }

    window.addEventListener("online", updateStatus);
    window.addEventListener("offline", updateStatus);

    return () => {
      window.removeEventListener("online", updateStatus);
      window.removeEventListener("offline", updateStatus);
    };
  }, []);

  return <p role="status">{online ? "Online" : "Offline"}</p>;
}
~~~

## 10. Refs and DOM integration

~~~jsx
import { useRef } from "react";

function SearchBox() {
  const inputRef = useRef(null);

  function focusSearch() {
    inputRef.current?.focus();
  }

  return (
    <section>
      <label htmlFor="site-search">Search</label>
      <input id="site-search" ref={inputRef} />
      <button type="button" onClick={focusSearch}>
        Focus search
      </button>
    </section>
  );
}
~~~

## 11. Custom hooks and hook rules

~~~jsx
import { useEffect, useState } from "react";

function useOnlineStatus() {
  const [isOnline, setIsOnline] = useState(navigator.onLine);

  useEffect(() => {
    const setOnline = () => setIsOnline(true);
    const setOffline = () => setIsOnline(false);

    window.addEventListener("online", setOnline);
    window.addEventListener("offline", setOffline);

    return () => {
      window.removeEventListener("online", setOnline);
      window.removeEventListener("offline", setOffline);
    };
  }, []);

  return isOnline;
}

function StatusBadge() {
  const isOnline = useOnlineStatus();
  return <p role="status">{isOnline ? "Connected" : "Offline"}</p>;
}
~~~

## 12. Suspense, lazy loading, and code splitting

~~~jsx
import { lazy, Suspense, useState } from "react";

const ReportsPage = lazy(() => import("./ReportsPage.jsx"));

function App() {
  const [showReports, setShowReports] = useState(false);

  return (
    <main>
      <button onClick={() => setShowReports(true)}>Open reports</button>
      {showReports && (
        <Suspense fallback={<p role="status">Loading reports...</p>}>
          <ReportsPage />
        </Suspense>
      )}
    </main>
  );
}
~~~

## 13. Error boundaries and recovery

~~~jsx
import { Component } from "react";

class ErrorBoundary extends Component {
  state = { hasError: false };

  static getDerivedStateFromError() {
    return { hasError: true };
  }

  render() {
    if (this.state.hasError) {
      return (
        <section role="alert">
          <h2>This section could not be displayed.</h2>
          <button onClick={() => this.setState({ hasError: false })}>
            Try again
          </button>
        </section>
      );
    }

    return this.props.children;
  }
}
~~~

~~~jsx
<ErrorBoundary>
  <ReportsPanel />
</ErrorBoundary>
~~~

## 14. React 19 actions and optimistic updates

~~~jsx
import { useActionState } from "react";

async function saveName(previousState, formData) {
  const name = String(formData.get("name") || "").trim();

  if (name.length < 2) {
    return { message: "Enter a name with at least two characters." };
  }

  await Promise.resolve();
  return { message: "Saved " + name + "." };
}

function NameForm() {
  const [state, formAction, isPending] = useActionState(saveName, {
    message: "",
  });

  return (
    <form action={formAction}>
      <label htmlFor="name">Name</label>
      <input id="name" name="name" required />
      <button disabled={isPending}>
        {isPending ? "Saving..." : "Save"}
      </button>
      <p role="status">{state.message}</p>
    </form>
  );
}
~~~

## 15. Accessibility, transitions, and performance

~~~jsx
function SearchForm({ onSearch }) {
  function handleSubmit(event) {
    event.preventDefault();
    const formData = new FormData(event.currentTarget);
    onSearch(String(formData.get("query") || ""));
  }

  return (
    <form onSubmit={handleSubmit}>
      <label htmlFor="query">Search products</label>
      <input id="query" name="query" type="search" />
      <button type="submit">Search</button>
    </form>
  );
}
~~~

~~~jsx
import { useState, useTransition } from "react";

function FilterPanel({ items }) {
  const [query, setQuery] = useState("");
  const [filter, setFilter] = useState("");
  const [isPending, startTransition] = useTransition();

  function handleChange(event) {
    const value = event.target.value;
    setQuery(value);
    startTransition(() => setFilter(value));
  }

  const results = items.filter((item) =>
    item.name.toLowerCase().includes(filter.toLowerCase())
  );

  return (
    <section>
      <label htmlFor="filter">Filter items</label>
      <input id="filter" value={query} onChange={handleChange} />
      {isPending && <p role="status">Updating results...</p>}
      <p>{results.length} results</p>
    </section>
  );
}
~~~

| [Previous: Accessibility, transitions, and performance](15-accessibility-transitions-and-performance.md) | [Notes index](../README.md) | [Next: Complete questions and answers](99-complete-q-and-a.md) |
|:--|:--:|--:|
