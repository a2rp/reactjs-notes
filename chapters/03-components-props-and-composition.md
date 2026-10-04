# 3. Components, props, and composition

[Back to notes index](../README.md)

| [Previous: JSX and rendering](../chapters/02-jsx-and-rendering.md) | [Notes index](../README.md) | [Next: State and events](../chapters/04-state-and-events.md) |
|:--|:--:|--:|

## What I am learning here

A component is a function that returns a description of part of the interface. A page can be composed from small components such as a header, product card, form field, and footer. Each component should have a clear purpose and a useful name.

Props are inputs supplied by the parent. A child reads props to decide what to render. Data flows from parent to child, so a child should not modify the object it receives. To change shared data, the parent can pass a callback.

## Pass data through props

~~~jsx
function ProfileCard({ person, onOpen }) {
  return (
    <article className="profile-card">
      <h2>{person.name}</h2>
      <p>{person.role}</p>
      <button onClick={() => onOpen(person.id)}>View profile</button>
    </article>
  );
}

function Team({ people }) {
  function openProfile(id) {
    console.log("Open profile:", id);
  }

  return (
    <section>
      {people.map((person) => (
        <ProfileCard
          key={person.id}
          person={person}
          onOpen={openProfile}
        />
      ))}
    </section>
  );
}
~~~

Here, Team owns the collection and ProfileCard presents one person. The event callback travels down as a prop, and the child calls it with the selected ID. The parent decides what that event means.

## Compose with children

The special children prop contains the elements placed between a component's opening and closing tags. It is useful for reusable layout shells.

~~~jsx
function Panel({ title, children }) {
  return (
    <section className="panel">
      <h2>{title}</h2>
      <div>{children}</div>
    </section>
  );
}

function Summary() {
  return (
    <Panel title="Today">
      <p>Three tasks are complete.</p>
    </Panel>
  );
}
~~~

Composition lets a component control shared structure while the caller supplies the specific content. Prefer a few meaningful props over one component that tries to handle unrelated cases through many flags.

## Questions to review

1. What does a component return?
2. Who supplies a component's props?
3. Why should a child avoid mutating props?
4. How can a child request that a parent change data?
5. What does the children prop represent?
6. When is composition useful?
7. Why should a component have a focused purpose?
8. Which component should own a collection displayed by several child cards?

| [Previous: JSX and rendering](../chapters/02-jsx-and-rendering.md) | [Notes index](../README.md) | [Next: State and events](../chapters/04-state-and-events.md) |
|:--|:--:|--:|

