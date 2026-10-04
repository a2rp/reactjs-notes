# 4. State and events

[Back to notes index](../README.md)

| [Previous: Components, props, and composition](../chapters/03-components-props-and-composition.md) | [Notes index](../README.md) | [Next: Conditional rendering, lists, and keys](../chapters/05-conditional-rendering-lists-and-keys.md) |
|:--|:--:|--:|

## What I am learning here

State is data that belongs to a component and can change over time. When state changes through its setter, React schedules another render using the new value. A normal local variable does not trigger a render, so it is not a replacement for state when the UI must respond to a change.

useState returns the current state value and a setter. A click handler can call the setter. React state behaves like a snapshot for the current render, so updates based on the previous value should use the updater form.

## Update state from an event

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

The function passed to setCount receives the latest queued value. This matters when several updates depend on one another. For example, two calls that each use count + 1 may both read the same render snapshot; two updater calls are applied in order.

## Replace objects and arrays

Treat state objects and arrays as read-only. Create a new value when changing one field.

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

Do not call push on a state array or assign directly to a state object. Mutating an existing value can make changes difficult for React and for the person reading the code to track.

Keep state as small as practical. Values that can be calculated from current props or state usually do not need a separate state variable.

## Questions to review

1. When is a value state instead of a regular variable?
2. What does the setter returned by useState do?
3. Why is state described as a render snapshot?
4. When should I use the updater form of a setter?
5. Why should state objects be replaced instead of mutated?
6. How can I update one matching item in an array immutably?
7. Why can duplicate derived state become inconsistent?
8. Which part of a component should usually handle a user event?

| [Previous: Components, props, and composition](../chapters/03-components-props-and-composition.md) | [Notes index](../README.md) | [Next: Conditional rendering, lists, and keys](../chapters/05-conditional-rendering-lists-and-keys.md) |
|:--|:--:|--:|

