# 15. Accessibility, transitions, and performance

[Back to notes index](../README.md)

| [Previous: React 19 actions and optimistic updates](../chapters/14-actions-and-optimistic-updates.md) | [Notes index](../README.md) | [Next: All code samples](../chapters/98-all-code-samples.md) |
|:--|:--:|--:|

## What I am learning here

A React interface should work for keyboard users, screen readers, touch input, and different viewport sizes. Semantic HTML gives controls their expected behavior. A real button is easier to use than a clickable div, and a label gives an input an accessible name.

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

Keep keyboard focus visible. Announce asynchronous status with a suitable live region, use headings in a meaningful order, and test controls without a mouse. Avoid using color as the only signal.

## Keep expensive updates responsive

A transition marks a non-urgent state update so React can keep urgent interactions responsive. It does not make the calculation itself faster, and it should not be used for a text input's immediate controlled value.

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

Measure before adding memoization. React Compiler can reduce the need for manual memoization in configured projects. useMemo and memo remain tools for measured cases, not defaults that every component needs. Clear state ownership, stable keys, and smaller component boundaries often solve update problems first.

## Questions to review

1. Why use a semantic button instead of a clickable div?
2. How should an input receive an accessible name?
3. Why should keyboard focus remain visible?
4. What kind of update is a transition for?
5. Should a controlled text input update as a transition?
6. Does useTransition make a slow calculation faster by itself?
7. When should manual memoization be added?
8. What should I measure before optimizing?

| [Previous: React 19 actions and optimistic updates](../chapters/14-actions-and-optimistic-updates.md) | [Notes index](../README.md) | [Next: All code samples](../chapters/98-all-code-samples.md) |
|:--|:--:|--:|

