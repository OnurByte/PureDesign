# Aligned Card Internals Without Height Measurement

## Compose

- [responsive auto-fit Grid](../primitives/responsive-grid-auto-fit.md)
- [`subgrid`](../primitives/subgrid.md)

When cards need aligned title/body/action rows despite different content lengths, use shared grid tracks rather than measuring sibling heights in JavaScript.

Conceptual shape:

```css
.cards {
  display: grid;
  grid-template-columns:
    repeat(auto-fit, minmax(min(16rem, 100%), 1fr));
}

.card {
  display: grid;
  grid-template-rows: subgrid;
  grid-row: span 3;
}
```

The exact parent track structure depends on the component, but the ownership rule is stable:

```text
alignment geometry -> Grid/Subgrid
content height      -> browser layout
application data    -> server
```

Do not add a resize observer whose only job is to copy the tallest title/footer height into every card.

Source: https://developer.mozilla.org/en-US/docs/Web/CSS/How_to/Layout_cookbook/Card
