# Container Style Queries

**Role:** derive descendant presentation from CSS-owned container state without JavaScript class propagation.

Current interoperable direction is primarily querying custom properties:

```css
.card {
  --density: compact;
}

@container style(--density: compact) {
  .card__meta {
    display: none;
  }
}
```

Unlike size queries, elements can act as style-query containers without setting `container-type`.

## Boundary

Support is less mature than container **size** queries, especially outside Chromium. Querying arbitrary regular properties remains an evolving area; current implementations are more limited than the full specification model.

Do not use this as the only route for conservative Firefox/Tor behavior. Prefer ordinary inheritance/custom properties as the baseline and treat style queries as progressive composition sugar.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Containment/Container_size_and_style_queries
- https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Containment/Container_queries
