# 11. Custom hooks and hook rules

[Back to notes index](../README.md)

| [Previous: Refs and DOM integration](../chapters/10-refs-and-dom-integration.md) | [Notes index](../README.md) | [Next: Suspense, lazy loading, and code splitting](../chapters/12-suspense-lazy-loading-and-code-splitting.md) |
|:--|:--:|--:|

## What I am learning here

A custom Hook is a JavaScript function whose name starts with use and that calls React Hooks. It lets me reuse stateful logic, such as subscribing to a browser event or managing a form field. Each component that calls a custom Hook gets its own Hook state unless both components intentionally read and update shared state through another mechanism.

Custom Hooks share logic, not a single state instance. A custom Hook can call other Hooks and can return values or callbacks that make the calling component simpler.

## Extract a reusable browser hook

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

## Follow the Hook rules

Call Hooks at the top level of a function component or custom Hook. Do not call them inside conditions, loops, nested functions, or event handlers. React relies on Hooks being called in the same order on each render.

Call Hooks only from React function components or custom Hooks. A regular helper function should remain an ordinary JavaScript function. A Hook linter can catch many incorrect call patterns and missing Effect dependencies.

Extract a custom Hook when it gives a useful name to reused stateful behavior. Avoid wrapping every line in a Hook when a plain helper function would do.

## Questions to review

1. What makes a function a custom Hook?
2. Do two components share one useState value because they call the same Hook?
3. What kind of logic is a custom Hook meant to reuse?
4. Where can a Hook be called?
5. Why must Hooks be called in a stable order?
6. Can an event handler call useState?
7. When is a plain helper function a better choice?
8. How does a Hook linter help?

| [Previous: Refs and DOM integration](../chapters/10-refs-and-dom-integration.md) | [Notes index](../README.md) | [Next: Suspense, lazy loading, and code splitting](../chapters/12-suspense-lazy-loading-and-code-splitting.md) |
|:--|:--:|--:|

