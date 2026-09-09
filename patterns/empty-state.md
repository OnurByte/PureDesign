# Empty State

## Prefer server-rendered semantics

If the application knows the result set is empty, render a real message:

```html
<section class="empty-state">
  <h2>No files yet</h2>
  <p>Upload a file to get started.</p>
</section>
```

This is the preferred path when the message is meaningful application content.

## Derived decorative state

For a container whose DOM emptiness is itself authoritative, CSS can observe [`:empty`](../primitives/empty-pseudo-class.md):

```css
.tag-list:empty {
  display: none;
}
```

or expose noncritical decoration without JS class toggling.

## State ownership

```text
whether records exist -> server
meaningful empty copy -> HTML
pure empty-container presentation -> :empty / CSS
```

Do not rely on pseudo-element `content` as the sole accessible status message for a critical empty state.
