# 10. Refs and DOM integration

[Back to notes index](../README.md)

| [Previous: Effects and external systems](../chapters/09-effects-and-external-systems.md) | [Notes index](../README.md) | [Next: Custom hooks and hook rules](../chapters/11-custom-hooks-and-hook-rules.md) |
|:--|:--:|--:|

## What I am learning here

A ref stores a value that persists between renders without causing another render when it changes. Refs are useful for a DOM node, timer ID, or other mutable value that is not itself displayed in the UI. If a value should change what the screen shows, it usually belongs in state instead.

## Focus an input

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

The ref object is stable across renders. React assigns the input DOM node to current after mounting and clears it when that node is removed. The optional chaining avoids calling focus when the node is not available.

Use DOM refs for direct browser tasks that React does not express well, such as focusing an input, measuring an element, or integrating a widget. Prefer state and props for visible content. Directly changing text or children behind React's back can cause the DOM to disagree with the next render.

A ref can also keep a timer ID so an event handler can cancel it later. Do not read or write a ref during rendering to decide visible output.

## Questions to review

1. What kind of value belongs in a ref?
2. Does changing ref.current trigger a render?
3. What does React place in a DOM ref after mounting?
4. Why can optional chaining be useful when focusing a ref?
5. When should visible content use state instead of a ref?
6. Name one browser task where a DOM ref is useful.
7. Why should I avoid changing rendered children directly?
8. What is a reasonable non-DOM value to store in a ref?

| [Previous: Effects and external systems](../chapters/09-effects-and-external-systems.md) | [Notes index](../README.md) | [Next: Custom hooks and hook rules](../chapters/11-custom-hooks-and-hook-rules.md) |
|:--|:--:|--:|

