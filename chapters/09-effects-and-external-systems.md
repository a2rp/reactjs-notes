# 9. Effects and external systems

[Back to notes index](../README.md)

| [Previous: Reducers and context](../chapters/08-reducers-and-context.md) | [Notes index](../README.md) | [Next: Refs and DOM integration](../chapters/10-refs-and-dom-integration.md) |
|:--|:--:|--:|

## What I am learning here

An Effect synchronizes a component with something outside React, such as a browser event, timer, connection, or third-party widget. Effects run after React commits the screen. They are not needed for ordinary calculations that can happen while rendering or for user actions that belong in an event handler.

## Subscribe and clean up

~~~jsx
import { useEffect, useState } from "react";

function OnlineStatus() {
  const [online, setOnline] = useState(navigator.onLine);

  useEffect(() => {
    function updateStatus() {
      setOnline(navigator.onLine);
    }

    window.addEventListener("online", updateStatus);
    window.addEventListener("offline", updateStatus);

    return () => {
      window.removeEventListener("online", updateStatus);
      window.removeEventListener("offline", updateStatus);
    };
  }, []);

  return <p role="status">{online ? "Online" : "Offline"}</p>;
}
~~~

The cleanup removes the same listeners that setup added. Cleanup matters when dependencies change and when a component leaves the screen. It prevents duplicate subscriptions and stale work.

The dependency list tells React which reactive values the Effect uses. Include every value read from the component scope. If the list feels unstable, restructure the code so the Effect depends on the actual external input. Do not silence a dependency warning by guessing.

For data loading, handle loading, success, and error states. If the request can outlive the screen or a newer request, cancel it with AbortController or ignore its stale result during cleanup. Avoid an Effect that only copies one state value into another; derive that value instead.

## Questions to review

1. What kind of work belongs in an Effect?
2. Why should simple derived values avoid Effects?
3. When does an Effect cleanup run?
4. What does the dependency list describe?
5. Why remove event listeners during cleanup?
6. What can happen if an old request updates a newer screen?
7. Which tool can cancel a fetch request?
8. Where should work caused by a button click usually run?

| [Previous: Reducers and context](../chapters/08-reducers-and-context.md) | [Notes index](../README.md) | [Next: Refs and DOM integration](../chapters/10-refs-and-dom-integration.md) |
|:--|:--:|--:|

