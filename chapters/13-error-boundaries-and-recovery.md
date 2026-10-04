# 13. Error boundaries and recovery

[Back to notes index](../README.md)

| [Previous: Suspense, lazy loading, and code splitting](../chapters/12-suspense-lazy-loading-and-code-splitting.md) | [Notes index](../README.md) | [Next: React 19 actions and optimistic updates](../chapters/14-actions-and-optimistic-updates.md) |
|:--|:--:|--:|

## What I am learning here

An Error Boundary catches errors thrown while its child tree renders and shows a fallback instead of removing the whole interface. React's built-in Error Boundary API is implemented with a class component. I can put one around a section that can fail independently, such as a report panel.

Error Boundaries do not catch errors from event handlers, ordinary asynchronous callbacks, or the boundary itself. Those errors need their own handling. A failed save should usually set an error state near the form that performed the save.

## Add a boundary around a risky section

~~~jsx
import { Component } from "react";

class ErrorBoundary extends Component {
  state = { hasError: false };

  static getDerivedStateFromError() {
    return { hasError: true };
  }

  render() {
    if (this.state.hasError) {
      return (
        <section role="alert">
          <h2>This section could not be displayed.</h2>
          <button onClick={() => this.setState({ hasError: false })}>
            Try again
          </button>
        </section>
      );
    }

    return this.props.children;
  }
}
~~~

Wrap the part that needs a separate fallback:

~~~jsx
<ErrorBoundary>
  <ReportsPanel />
</ErrorBoundary>
~~~

A retry only helps if the cause can change or the failed tree is reset. For example, the parent can change a key to remount a section after its input or route changes. In a real application, log useful error details to a trusted error service while showing a calm, actionable message to the user.

## Questions to review

1. Which rendering failures can an Error Boundary catch?
2. What does the fallback replace?
3. Why use a boundary around a section instead of every tiny component?
4. Does a boundary catch a click handler exception?
5. Where should a failed form submission be handled?
6. Which lifecycle API lets a class boundary switch to fallback state?
7. When can a retry be useful?
8. What should an error message help the user do?

| [Previous: Suspense, lazy loading, and code splitting](../chapters/12-suspense-lazy-loading-and-code-splitting.md) | [Notes index](../README.md) | [Next: React 19 actions and optimistic updates](../chapters/14-actions-and-optimistic-updates.md) |
|:--|:--:|--:|

