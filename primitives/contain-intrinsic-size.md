# `contain-intrinsic-size`

**Role:** give the browser a fallback/remembered size for content that is skipped because of containment.

Common pairing:

```css
.message {
  content-visibility: auto;
  contain-intrinsic-size: auto 6rem;
}
```

The `auto <length>` form lets the browser use the supplied estimate until the element is rendered, then remember and reuse the real size where supported.

## Why

Without a useful intrinsic-size placeholder, off-screen render skipping can cause poor scrollbar estimates or layout jumps when skipped content becomes visible.

This replaces JavaScript techniques that pre-measure every item purely to reserve layout space.

## Boundary

This is a rendering/layout hint, not data virtualization:

```text
DOM nodes still exist
response bytes still exist
server pagination still matters
```

Use it with [`content-visibility.md`](content-visibility.md), not instead of server-side limits.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/contain-intrinsic-size
- https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Containment/Using
