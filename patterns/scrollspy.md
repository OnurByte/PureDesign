# Scrollspy / Active Table of Contents

## Baseline

Use ordinary anchor navigation. The page remains usable without automatic active-section highlighting.

## Enhancement

Compose:

- [`scroll-target-group` + `:target-current`](../primitives/scroll-target-group.md)
- optional [CSS Anchor Positioning](../primitives/anchor-positioning.md) for a moving visual indicator
- optional [`:has()`](../primitives/has.md) for derived parent styling

```css
.toc {
  scroll-target-group: auto;
}

.toc a:target-current {
  font-weight: 700;
}
```

## Replaces

For supporting browsers, this can remove the `IntersectionObserver -> calculate active -> toggle .active` script.

## Rule

Automatic highlighting is enhancement. Navigation links themselves must remain normal working anchors.
