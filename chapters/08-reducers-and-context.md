# 8. Reducers and context

[Back to notes index](../README.md)

| [Previous: State design and lifting state](../chapters/07-state-design-and-lifting-state.md) | [Notes index](../README.md) | [Next: Effects and external systems](../chapters/09-effects-and-external-systems.md) |
|:--|:--:|--:|

## What I am learning here

useReducer is useful when state transitions have several related cases or when many event handlers update the same state. A reducer receives the current state and an action, then returns the next state. It must be pure: it should not change the current state or perform network requests.

Context passes a value through a component tree without threading the same prop through every layer. It works well for values such as the current theme or signed-in user. Context is not automatically the right place for every changing value.

## Describe updates with actions

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

The action names make the available state transitions visible. For more complex state, keep each case focused and return new arrays or objects instead of mutating existing values.

## Share a stable value with context

Create a context, provide it above the consumers, and read it with useContext. Keep the provider near the components that need the value. If a context value is recreated every render, many consumers may update; consider whether its value can be split or kept stable.

Use props when the relationship is direct and easy to follow. Use context when many levels need the same value. Avoid using context as an unstructured global container.

## Questions to review

1. What does a reducer receive and return?
2. Why must a reducer be pure?
3. What is an action?
4. When can useReducer make updates easier to understand?
5. What problem does context solve?
6. Which values are reasonable context candidates?
7. Why should context providers stay near their consumers?
8. When are props simpler than context?

| [Previous: State design and lifting state](../chapters/07-state-design-and-lifting-state.md) | [Notes index](../README.md) | [Next: Effects and external systems](../chapters/09-effects-and-external-systems.md) |
|:--|:--:|--:|

