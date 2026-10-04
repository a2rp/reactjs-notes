# 6. Forms and validation

[Back to notes index](../README.md)

| [Previous: Conditional rendering, lists, and keys](../chapters/05-conditional-rendering-lists-and-keys.md) | [Notes index](../README.md) | [Next: State design and lifting state](../chapters/07-state-design-and-lifting-state.md) |
|:--|:--:|--:|

## What I am learning here

A form collects user input. A controlled input receives its value from React state and reports edits through an event handler. This keeps the displayed value and the component's data aligned. Small forms are easier to reason about when each field has a clear value, label, and validation message.

## Build a controlled form

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

The browser provides useful built-in checks for required fields and email syntax. Application validation can add rules the browser cannot know. For production data, the server must validate too because browser checks can be bypassed.

Use a label connected to each input. If a field has an error, associate the message with the field using aria-describedby and mark the invalid field with aria-invalid. Do not communicate an error by color alone. Keep the entered value when validation fails so the person does not need to type it again.

## Questions to review

1. What makes an input controlled?
2. Which event provides the updated text value?
3. Why does a form handler call preventDefault?
4. What validation can the browser provide?
5. Why must the server also validate submitted data?
6. How should a label be connected to its input?
7. How can an error message be associated with a field?
8. Why should invalid submission preserve the user's input?

| [Previous: Conditional rendering, lists, and keys](../chapters/05-conditional-rendering-lists-and-keys.md) | [Notes index](../README.md) | [Next: State design and lifting state](../chapters/07-state-design-and-lifting-state.md) |
|:--|:--:|--:|

