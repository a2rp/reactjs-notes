# 2. JSX and rendering

[Back to notes index](../README.md)

| [Previous: React foundations and project setup](../chapters/01-react-foundations-and-setup.md) | [Notes index](../README.md) | [Next: Components, props, and composition](../chapters/03-components-props-and-composition.md) |
|:--|:--:|--:|

## What I am learning here

JSX lets a component describe a tree of browser elements with syntax that looks like HTML. It is JavaScript syntax transformed by the build step, so JSX can use JavaScript values and functions. It is not a string of HTML.

A JSX expression must have one enclosing element. Every element must be closed, and attributes use JavaScript property names such as className and htmlFor. Text is written directly. JavaScript expressions are placed inside braces.

## Put values into the UI

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

The braces contain expressions that produce values. They do not contain statements such as if or for. A ternary expression is useful for a small choice. For more involved decisions, calculate a value before the return or split the UI into a component.

Event attributes receive a function. Passing handleSave runs it later when the event happens. Writing handleSave() runs it while rendering, which is usually a mistake.

~~~jsx
function SaveButton() {
  function handleSave() {
    console.log("Saved");
  }

  return <button onClick={handleSave}>Save</button>;
}
~~~

## Keep rendering safe and readable

React renders text as text, which helps prevent accidental interpretation of user input as markup. Avoid inserting untrusted HTML with dangerouslySetInnerHTML. Use semantic elements that describe the content, and keep complex calculations out of the JSX when a named variable would make the result easier to understand.

A component renders again when React receives updated props or state. Rendering should describe the current UI without changing external data. Browser updates are applied after React evaluates the component tree.

## Questions to review

1. What is JSX used for?
2. Why must JSX elements be closed?
3. How do I insert a JavaScript value into JSX?
4. Why does JSX use className?
5. What is the difference between handleSave and handleSave() in an event prop?
6. When is a ternary expression useful in JSX?
7. How does React treat ordinary text values?
8. Why should rendering avoid changing external data?

| [Previous: React foundations and project setup](../chapters/01-react-foundations-and-setup.md) | [Notes index](../README.md) | [Next: Components, props, and composition](../chapters/03-components-props-and-composition.md) |
|:--|:--:|--:|

