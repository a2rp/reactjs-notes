# 5. Conditional rendering, lists, and keys

[Back to notes index](../README.md)

| [Previous: State and events](../chapters/04-state-and-events.md) | [Notes index](../README.md) | [Next: Forms and validation](../chapters/06-forms-and-validation.md) |
|:--|:--:|--:|

## What I am learning here

A component can choose what to render using normal JavaScript conditions. A list can be transformed into elements with map. Stable keys let React match an item with its previous rendered version when the list changes.

## Choose a view for the current state

Use an early return when the whole component has a distinct loading or empty state. Use a conditional expression for a short inline choice.

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

For optional content, logical AND is concise when the condition is definitely boolean:

~~~jsx
{isAdmin && <a href="/settings">Settings</a>}
~~~

Avoid using an arbitrary number with && when zero could be rendered. Write an explicit boolean comparison or use a ternary.

## Render a list with stable identity

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

Keys should be stable among renders and unique among siblings. A database ID or permanent identifier is a good key. The array index can point to the wrong item after insertion, deletion, filtering, or reordering, so it is suitable only for a truly static list that never changes order.

Keys are used by React to track identity. They are not passed as a regular prop. If the child needs the ID, pass it separately.

## Questions to review

1. How can a component show a loading state?
2. When is an early return easy to read?
3. What does map produce in a rendered list?
4. What job does a key perform?
5. Why is a stable data ID a good key?
6. What can go wrong when a changing list uses array indexes as keys?
7. Is a key passed to the child as a normal prop?
8. How can I avoid rendering a zero with logical AND?

| [Previous: State and events](../chapters/04-state-and-events.md) | [Notes index](../README.md) | [Next: Forms and validation](../chapters/06-forms-and-validation.md) |
|:--|:--:|--:|

