# Container Size Queries

**Role:** component responsiveness owned by CSS instead of `ResizeObserver`.

```css
.card-shell {
  container-type: inline-size;
}

@container (width < 32rem) {
  .card {
    grid-template-columns: 1fr;
  }
}
```

Use when the HTML stays the same and only presentation changes with the component's available size.

## Replaces

```text
ResizeObserver
 -> read width
 -> toggle small/large class
 -> CSS
```

with:

```text
container width -> @container -> CSS
```

## Boundary

Container queries do **not** replace JavaScript when width changes data, templates, chart calculations, child props, or other application behavior.

A 2026 CleverCloud issue documents exactly this migration boundary and lists components that can and cannot move from a resize controller to native queries.

## Compatibility

Firefox supports size container queries by default since Firefox 110, so they are inside the Firefox 140 ESR engine baseline.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/container-type
- https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/110
- https://github.com/CleverCloud/clever-components/issues/1657
- https://www.reddit.com/r/css/comments/1sdpeaj/
