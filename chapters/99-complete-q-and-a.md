# 17. Complete questions and answers

[Back to notes index](../README.md)

| [Previous: All code samples](98-all-code-samples.md) | [Notes index](../README.md) | [Next: Notes index](../README.md) |
|:--|:--:|--:|

## 1. React foundations and project setup

**1. What kind of problem is React designed to help solve?**

React is a JavaScript library for describing and updating user interfaces.

**2. What does a component describe?**

A component returns a description of the UI for its current inputs and state.

**3. Why does a React project need a browser entry point?**

The entry point connects the component tree to an element in the browser document.

**4. What job does the root HTML element perform?**

The root element is the mount point where React manages the rendered tree.

**5. Why is the root normally created once?**

Create one root for the page element so React can manage updates consistently.

**6. What information belongs in the package file?**

The package file records project scripts, dependencies, and package metadata.

**7. What should I check when the first screen is blank?**

Check the browser console, development terminal, root ID, and imports for startup errors.

**8. Does React require a particular router or styling system?**

No. React can be used with different routers, styling systems, and build tools.

## 2. JSX and rendering

**9. What is JSX used for?**

JSX describes UI elements inside JavaScript.

**10. Why must JSX elements be closed?**

Balanced opening and closing tags make the element tree valid.

**11. How do I insert a JavaScript value into JSX?**

Place an expression between braces inside JSX.

**12. Why does JSX use className?**

className is the JavaScript property name React uses for an element class attribute.

**13. What is the difference between handleSave and handleSave() in an event prop?**

Passing the function defers it until the event; calling it executes it during render.

**14. When is a ternary expression useful in JSX?**

A ternary is useful for a short choice between two rendered values.

**15. How does React treat ordinary text values?**

React renders ordinary strings as text rather than interpreting them as markup.

**16. Why should rendering avoid changing external data?**

Rendering should be repeatable and free of external mutations so React can reconcile predictably.

## 3. Components, props, and composition

**17. What does a component return?**

A component returns React nodes that describe part of the interface.

**18. Who supplies a component's props?**

The parent component supplies a child's props.

**19. Why should a child avoid mutating props?**

Props are inputs, so changing them in a child would break the parent's ownership.

**20. How can a child request that a parent change data?**

Pass a callback prop that the child can call to request a change.

**21. What does the children prop represent?**

children contains the nested content between a component's tags.

**22. When is composition useful?**

Composition lets a caller provide content inside reusable structure.

**23. Why should a component have a focused purpose?**

A focused component has a clear job and is easier to understand and reuse.

**24. Which component should own a collection displayed by several child cards?**

The nearest parent that owns the shared collection should map it into child cards.

## 4. State and events

**25. When is a value state instead of a regular variable?**

A value is state when changes to it should cause the UI to render again.

**26. What does the setter returned by useState do?**

The setter queues a new state value and schedules React to render with it.

**27. Why is state described as a render snapshot?**

A render sees a fixed state snapshot; setters affect a later render.

**28. When should I use the updater form of a setter?**

Use an updater when the next value depends on the previous state.

**29. Why should state objects be replaced instead of mutated?**

Replacing objects creates a new value that React and readers can track clearly.

**30. How can I update one matching item in an array immutably?**

Use map to return a new array with the matching item replaced.

**31. Why can duplicate derived state become inconsistent?**

Duplicated derived values can drift out of sync when their source changes.

**32. Which part of a component should usually handle a user event?**

Event handlers should handle user actions and call the appropriate state setter.

## 5. Conditional rendering, lists, and keys

**33. How can a component show a loading state?**

Use a condition to choose between loading, error, empty, or ready UI.

**34. When is an early return easy to read?**

An early return is clear when one state replaces the entire component output.

**35. What does map produce in a rendered list?**

map transforms each data item into a rendered element.

**36. What job does a key perform?**

A key helps React match a child with its identity across list renders.

**37. Why is a stable data ID a good key?**

A stable data ID stays associated with the same item as order changes.

**38. What can go wrong when a changing list uses array indexes as keys?**

Indexes shift when items are inserted, removed, or reordered, so state can attach to the wrong item.

**39. Is a key passed to the child as a normal prop?**

No. key is reserved for React reconciliation and is not forwarded as a prop.

**40. How can I avoid rendering a zero with logical AND?**

Compare a number explicitly, such as count > 0, before using logical AND.

## 6. Forms and validation

**41. What makes an input controlled?**

A controlled input gets its current value from React state.

**42. Which event provides the updated text value?**

The change handler reads event.target.value and updates state.

**43. Why does a form handler call preventDefault?**

preventDefault stops the browser's default page navigation for that submission.

**44. What validation can the browser provide?**

The browser can enforce basic constraints such as required fields and email format.

**45. Why must the server also validate submitted data?**

Client checks can be bypassed, so the server must validate submitted data itself.

**46. How should a label be connected to its input?**

Use a label with htmlFor matching the input's id.

**47. How can an error message be associated with a field?**

Set aria-describedby to the ID of the error text and mark invalid fields appropriately.

**48. Why should invalid submission preserve the user's input?**

Keeping the typed value lets the person correct a problem without starting over.

## 7. State design and lifting state

**49. What does it mean to keep state minimal?**

Minimal state stores only values that must change independently.

**50. Which values can usually be derived during render?**

Calculate a value during render when it follows directly from current props or state.

**51. What problem can duplicate state create?**

Store source values and derive filtered, formatted, or counted values from them.

**52. When should state move to a common parent?**

Move shared state to the nearest common parent of the components that need it.

**53. How does the parent keep two children in sync?**

Pass the current value and an update callback from the owner to both children.

**54. Should every state value live at the top of the application?**

No. Place each state value near the components that use it.

**55. Where should input-only state usually live?**

Input-only state usually belongs in the component that renders and controls that input.

**56. When might a server cache be a better place for remote data?**

A server cache helps manage remote data, request status, and revalidation.

## 8. Reducers and context

**57. What does a reducer receive and return?**

A reducer receives the current state and an action, then returns the next state.

**58. Why must a reducer be pure?**

A pure reducer avoids side effects and always computes the result from its inputs.

**59. What is an action?**

An action describes an update the application wants to perform.

**60. When can useReducer make updates easier to understand?**

useReducer helps when multiple related transitions should be described in one place.

**61. What problem does context solve?**

Context makes a value available to descendants without repeated intermediate props.

**62. Which values are reasonable context candidates?**

Theme and signed-in user are examples when many descendants need them.

**63. Why should context providers stay near their consumers?**

A nearby provider limits which parts of the tree depend on that context.

**64. When are props simpler than context?**

Props are simpler for direct parent-child data flow.

## 9. Effects and external systems

**65. What kind of work belongs in an Effect?**

An Effect synchronizes React with an external system such as a listener or connection.

**66. Why should simple derived values avoid Effects?**

Derived calculations can run during render and do not need an Effect.

**67. When does an Effect cleanup run?**

Cleanup runs before an Effect restarts and when its component is removed.

**68. What does the dependency list describe?**

Dependencies describe reactive values read by the Effect.

**69. Why remove event listeners during cleanup?**

Removing listeners prevents duplicate subscriptions and callbacks after unmount.

**70. What can happen if an old request updates a newer screen?**

A stale request can show data for an older selection on the newer screen.

**71. Which tool can cancel a fetch request?**

AbortController can signal fetch to cancel a request.

**72. Where should work caused by a button click usually run?**

Work directly caused by a click belongs in that event handler.

## 10. Refs and DOM integration

**73. What kind of value belongs in a ref?**

A ref stores a mutable value across renders without scheduling a render when it changes.

**74. Does changing ref.current trigger a render?**

No. Changing current does not schedule a render.

**75. What does React place in a DOM ref after mounting?**

React assigns the mounted DOM node to current.

**76. Why can optional chaining be useful when focusing a ref?**

The node can be absent before mounting or after unmounting, so optional chaining avoids an error.

**77. When should visible content use state instead of a ref?**

Use state for visible content because state changes trigger a render.

**78. Name one browser task where a DOM ref is useful.**

Focusing an input, measuring an element, or controlling a widget can use a DOM ref.

**79. Why should I avoid changing rendered children directly?**

React may later render over direct DOM changes, causing the displayed tree to disagree.

**80. What is a reasonable non-DOM value to store in a ref?**

A timer ID is a non-DOM value that can be kept in a ref.

## 11. Custom hooks and hook rules

**81. What makes a function a custom Hook?**

A custom Hook is a function named with the use prefix that calls other Hooks.

**82. Do two components share one useState value because they call the same Hook?**

No. Each caller has an independent Hook state unless they use shared state elsewhere.

**83. What kind of logic is a custom Hook meant to reuse?**

Custom Hooks reuse stateful behavior and its synchronization logic.

**84. Where can a Hook be called?**

Call Hooks at the top level of function components and custom Hooks.

**85. Why must Hooks be called in a stable order?**

Stable call order lets React associate Hook state with the correct call.

**86. Can an event handler call useState?**

No. Hooks cannot be called inside event handlers.

**87. When is a plain helper function a better choice?**

A plain helper is better for pure calculations that do not use React state or Hooks.

**88. How does a Hook linter help?**

The linter catches invalid call positions and missing reactive dependencies.

## 12. Suspense, lazy loading, and code splitting

**89. What problem does code splitting address?**

Code splitting lets the browser load less-used component code only when needed.

**90. What does React.lazy receive?**

lazy receives a loader function that returns a Promise for a component module.

**91. Where should a lazy component be declared?**

Declare lazy components outside rendering functions so their identity stays stable.

**92. What does Suspense render while its child is waiting?**

Suspense renders its fallback until its child can be shown.

**93. Why should a fallback communicate loading?**

A useful fallback tells people that content is loading and reserves suitable space.

**94. Does Suspense detect every ordinary fetch call?**

No. Ordinary fetch calls do not automatically suspend a component.

**95. Where should a Suspense boundary be placed?**

Place a boundary around the section whose loading can be handled independently.

**96. What export does the common lazy import pattern expect?**

The standard lazy pattern expects the imported module to provide a default component export.

## 13. Error boundaries and recovery

**97. Which rendering failures can an Error Boundary catch?**

An Error Boundary catches errors thrown while its descendants render.

**98. What does the fallback replace?**

It replaces the failed descendant UI with a fallback.

**99. Why use a boundary around a section instead of every tiny component?**

A section boundary lets the rest of the page remain usable.

**100. Does a boundary catch a click handler exception?**

No. Event-handler errors need handling in the handler's own flow.

**101. Where should a failed form submission be handled?**

Handle a save failure near its form, where the user can see and correct it.

**102. Which lifecycle API lets a class boundary switch to fallback state?**

static getDerivedStateFromError returns state that causes the fallback render.

**103. When can a retry be useful?**

Retry helps when the cause can change or the failed tree is reset.

**104. What should an error message help the user do?**

Give a calm explanation and a useful next action when possible.

## 14. React 19 actions and optimistic updates

**105. What does a form Action handle?**

An Action handles work started by a form submission or transition.

**106. What values does useActionState return?**

useActionState returns the current result, a form action function, and a pending flag.

**107. What is FormData used for?**

FormData provides the named values submitted by a form.

**108. Why is server-side validation still required?**

Server validation is required because client checks are not a security boundary.

**109. What does the pending flag communicate?**

The pending flag communicates that the action has not finished.

**110. What is an optimistic update?**

An optimistic update shows the expected result while a request is in progress.

**111. When should a client avoid marking an action as confirmed?**

Do not claim a payment or security-sensitive change succeeded before the server confirms it.

**112. How should a failed server request affect optimistic UI?**

On failure, restore confirmed data and explain the failure so the user can retry.

## 15. Accessibility, transitions, and performance

**113. Why use a semantic button instead of a clickable div?**

A semantic button provides built-in keyboard and activation behavior.

**114. How should an input receive an accessible name?**

Connect a label to an input with matching htmlFor and id values.

**115. Why should keyboard focus remain visible?**

Visible focus shows keyboard users which control is currently active.

**116. What kind of update is a transition for?**

A transition marks non-urgent rendering work that can be interrupted by urgent updates.

**117. Should a controlled text input update as a transition?**

No. Keep a controlled text field responsive with its immediate state update.

**118. Does useTransition make a slow calculation faster by itself?**

No. It changes scheduling priority, not the cost of the calculation itself.

**119. When should manual memoization be added?**

Add manual memoization after identifying a measured update or calculation problem.

**120. What should I measure before optimizing?**

Use profiling and realistic interaction measurements before optimizing.

## Cross-topic review

**121. Why should a list key stay stable?**

A stable key preserves the identity of the same item when the list changes order or membership.

**122. When should I use useEffect for a derived value?**

Usually never. Calculate the value from current props and state during rendering.

**123. How do context and props differ?**

Props express direct relationships; context supplies a value to descendants across many layers.

**124. What is the purpose of a reducer action?**

It names the event or intent that should produce a state transition.

**125. What should happen when an optimistic save fails?**

Show the confirmed value again and provide clear error feedback.

**126. What does a Suspense fallback represent?**

Temporary UI shown while supported child work, such as lazy code, is not ready.

**127. Why not memoize every component?**

Memoization adds complexity and helps only when it prevents measured, meaningful work.

**128. What is the difference between client validation and server validation?**

Client validation improves feedback; server validation protects the data boundary.

| [Previous: All code samples](98-all-code-samples.md) | [Notes index](../README.md) | [Next: Notes index](../README.md) |
|:--|:--:|--:|
