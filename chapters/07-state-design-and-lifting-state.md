# 7. State design and lifting state

[Back to notes index](../README.md)

| [Previous: Forms and validation](../chapters/06-forms-and-validation.md) | [Notes index](../README.md) | [Next: Reducers and context](../chapters/08-reducers-and-context.md) |
|:--|:--:|--:|

## What I am learning here

Good state design starts by deciding which values must change independently. Store the smallest set of values needed to describe the interface. Calculate values that can be derived from props or existing state instead of storing a second copy.

If two sibling components must stay in sync, move their shared state to their nearest common parent. The parent passes the current value and callbacks down. This pattern is called lifting state up.

## Store source values and derive the rest

~~~jsx
function ProductSearch({ products }) {
  const [query, setQuery] = useState("");
  const normalizedQuery = query.trim().toLowerCase();

  const visibleProducts = products.filter((product) =>
    product.name.toLowerCase().includes(normalizedQuery)
  );

  return (
    <section>
      <label htmlFor="product-search">Search products</label>
      <input
        id="product-search"
        value={query}
        onChange={(event) => setQuery(event.target.value)}
      />
      <p>{visibleProducts.length} products found</p>
      <ul>
        {visibleProducts.map((product) => (
          <li key={product.id}>{product.name}</li>
        ))}
      </ul>
    </section>
  );
}
~~~

The query is the changing source value. The normalized query and filtered array can be calculated during render. Keeping all three in state would require synchronizing them after every edit and after product data changes.

When state is lifted, keep it as close as possible to the components that need it. State that belongs only to one input should stay local. State shared across a page can belong to that page. Data needed across many routes may need a broader store or server cache.

## Questions to review

1. What does it mean to keep state minimal?
2. Which values can usually be derived during render?
3. What problem can duplicate state create?
4. When should state move to a common parent?
5. How does the parent keep two children in sync?
6. Should every state value live at the top of the application?
7. Where should input-only state usually live?
8. When might a server cache be a better place for remote data?

| [Previous: Forms and validation](../chapters/06-forms-and-validation.md) | [Notes index](../README.md) | [Next: Reducers and context](../chapters/08-reducers-and-context.md) |
|:--|:--:|--:|

