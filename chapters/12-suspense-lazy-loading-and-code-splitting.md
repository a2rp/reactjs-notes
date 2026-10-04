# 12. Suspense, lazy loading, and code splitting

[Back to notes index](../README.md)

| [Previous: Custom hooks and hook rules](../chapters/11-custom-hooks-and-hook-rules.md) | [Notes index](../README.md) | [Next: Error boundaries and recovery](../chapters/13-error-boundaries-and-recovery.md) |
|:--|:--:|--:|

## What I am learning here

Code splitting lets the browser load some component code only when it is needed. React.lazy loads a component from a dynamic import. A Suspense boundary displays a fallback while that component's code is loading.

Declare a lazy component outside other components. The imported module must provide a default component export for the common lazy pattern.

## Load a page on demand

~~~jsx
import { lazy, Suspense, useState } from "react";

const ReportsPage = lazy(() => import("./ReportsPage.jsx"));

function App() {
  const [showReports, setShowReports] = useState(false);

  return (
    <main>
      <button onClick={() => setShowReports(true)}>Open reports</button>
      {showReports && (
        <Suspense fallback={<p role="status">Loading reports...</p>}>
          <ReportsPage />
        </Suspense>
      )}
    </main>
  );
}
~~~

The build tool can create a separate file for ReportsPage. The browser requests it when React first renders that component. The fallback should be understandable and should not shift the layout more than necessary.

Suspense only responds to work that is integrated with Suspense, such as a lazy component. It does not automatically detect every fetch call or image request. Place boundaries around meaningful parts of the interface so one slow section does not replace the entire page with a spinner.

## Questions to review

1. What problem does code splitting address?
2. What does React.lazy receive?
3. Where should a lazy component be declared?
4. What does Suspense render while its child is waiting?
5. Why should a fallback communicate loading?
6. Does Suspense detect every ordinary fetch call?
7. Where should a Suspense boundary be placed?
8. What export does the common lazy import pattern expect?

| [Previous: Custom hooks and hook rules](../chapters/11-custom-hooks-and-hook-rules.md) | [Notes index](../README.md) | [Next: Error boundaries and recovery](../chapters/13-error-boundaries-and-recovery.md) |
|:--|:--:|--:|

