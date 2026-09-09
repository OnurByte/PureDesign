# Name-Only Container Queries

**Role:** style a component according to which named container it lives inside, without measuring that container and without requiring a size condition.

```html
<aside class="sidebar">
  <article class="card">
    <h2>Account</h2>
    <p>Manage profile settings.</p>
  </article>
</aside>

<main class="content">
  <article class="card">
    <h2>Account</h2>
    <p>Manage profile settings.</p>
  </article>
</main>
```

```css
.sidebar {
  container-name: sidebar;
}

@container sidebar {
  .card {
    display: grid;
    gap: .5rem;
  }
}
```

The query asks only whether the component has an ancestor named `sidebar`. No width, style or scroll condition is evaluated.

## Why this matters

A reusable server-rendered component often needs a small presentation variant based on context:

```text
same component markup
  -> inside sidebar -> compact presentation
  -> elsewhere      -> normal presentation
```

That context does not need a JavaScript prop, DOM measurement, duplicated component template, or brittle selector chain.

Name-only queries are also different from size queries: assigning only `container-name` does not create size containment.

## Boundary

This is presentation context, not application authority. Do not encode permissions, workflow state or business rules in container names.

If ordinary selectors or `@scope` express the relationship more clearly, use them. Name-only queries are most useful when the same component can be placed under several reusable named contexts.

## Compatibility

This is **not** core for Tor Browser / Firefox 140 ESR.

Support landed in:

- Firefox 149;
- Chrome / Edge 148;
- Safari 26.4.

Use it as progressive presentation until the conservative target moves forward.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/container-name
- https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Containment/Container_queries
- https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/149
- https://developer.chrome.com/release-notes/148
- https://webkit.org/blog/17862/webkit-features-for-safari-26-4/
