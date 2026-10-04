# 1. React foundations and project setup

[Back to notes index](../README.md)

| [Previous: Notes index](../README.md) | [Notes index](../README.md) | [Next: JSX and rendering](02-jsx-and-rendering.md) |
|:--|:--:|--:|

## What I am learning here

React is a JavaScript library for building user interfaces from components. A component receives data, describes the interface for that data, and React updates the browser when the data changes. Thinking in components makes a screen easier to split, reuse, and test.

A React project normally has three parts: JavaScript source, a build tool that prepares the source for browsers, and a browser entry point that mounts the React tree into an HTML element. React itself does not prescribe a router, styling system, or server framework. I choose those when the application needs them.

## Start a small JavaScript project

Vite is one option for local development. From a terminal, create a JavaScript React project and start its development server:

~~~sh
npm create vite@latest hello-react -- --template react
cd hello-react
npm install
npm run dev
~~~

The command prints a local address. Open that address in a browser. Keep the generated package files because they record the scripts and dependencies used by the project. For an existing codebase, inspect its package file before adding another build tool.

## Mount the React tree

The HTML document provides a root element. JavaScript finds that element and asks React to render the app inside it.

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

A small component can return the first screen:

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

The root is normally created once for the page. Components below it form a tree. The browser still displays HTML elements, but React calculates how the rendered output should change when component data changes.

## Keep project responsibilities clear

- The HTML entry file gives the page its document shell and root element.
- The JavaScript entry file creates the React root.
- Components describe parts of the interface.
- The package file records scripts and dependencies.
- CSS controls visual presentation.

When the page is blank, check the browser console, the development terminal, the root element ID, and the import path. These checks often reveal a spelling or startup error quickly.

## Questions to review

1. What kind of problem is React designed to help solve?
2. What does a component describe?
3. Why does a React project need a browser entry point?
4. What job does the root HTML element perform?
5. Why is the root normally created once?
6. What information belongs in the package file?
7. What should I check when the first screen is blank?
8. Does React require a particular router or styling system?

| [Previous: Notes index](../README.md) | [Notes index](../README.md) | [Next: JSX and rendering](02-jsx-and-rendering.md) |
|:--|:--:|--:|
