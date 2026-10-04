# 14. React 19 actions and optimistic updates

[Back to notes index](../README.md)

| [Previous: Error boundaries and recovery](../chapters/13-error-boundaries-and-recovery.md) | [Notes index](../README.md) | [Next: Accessibility, transitions, and performance](../chapters/15-accessibility-transitions-and-performance.md) |
|:--|:--:|--:|

## What I am learning here

React 19 adds form Actions and Hooks that help coordinate pending, successful, and optimistic updates. An Action is a function used for work triggered by a form or transition. The browser's FormData contains submitted fields. The server still needs to check and save the data.

useActionState connects an Action to state and returns the current result, a form action, and a pending flag. This keeps feedback close to the form.

## Show action state in a form

~~~jsx
import { useActionState } from "react";

async function saveName(previousState, formData) {
  const name = String(formData.get("name") || "").trim();

  if (name.length < 2) {
    return { message: "Enter a name with at least two characters." };
  }

  await Promise.resolve();
  return { message: "Saved " + name + "." };
}

function NameForm() {
  const [state, formAction, isPending] = useActionState(saveName, {
    message: "",
  });

  return (
    <form action={formAction}>
      <label htmlFor="name">Name</label>
      <input id="name" name="name" required />
      <button disabled={isPending}>
        {isPending ? "Saving..." : "Save"}
      </button>
      <p role="status">{state.message}</p>
    </form>
  );
}
~~~

The example uses a resolved Promise to show the shape of an asynchronous Action. A real save should call an application service and handle server errors. Never treat client-side validation as a security boundary.

useOptimistic can show the expected result before a server request finishes. If the request fails, the UI returns to the confirmed value. Use it for a clear, temporary improvement such as showing a newly sent message immediately. Do not present an unconfirmed payment or security-sensitive result as complete.

## Questions to review

1. What does a form Action handle?
2. What values does useActionState return?
3. What is FormData used for?
4. Why is server-side validation still required?
5. What does the pending flag communicate?
6. What is an optimistic update?
7. When should a client avoid marking an action as confirmed?
8. How should a failed server request affect optimistic UI?

| [Previous: Error boundaries and recovery](../chapters/13-error-boundaries-and-recovery.md) | [Notes index](../README.md) | [Next: Accessibility, transitions, and performance](../chapters/15-accessibility-transitions-and-performance.md) |
|:--|:--:|--:|

