# Item-Count-Aware Layout

Use this only when a decorative/layout value genuinely depends on an item's sibling position or the number of direct siblings.

## Baseline first

Core layout should still use mature Grid/Flex behavior:

```css
.items {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(12rem, 1fr));
  gap: 1rem;
}
```

## Progressive enhancement

```css
@supports (width: calc(1px * sibling-count())) {
  .item {
    --i: sibling-index();
    --n: sibling-count();
    animation-delay: calc((var(--i) - 1) * 40ms);
  }
}
```

Good uses are visual staggering, radial decoration, proportional indicators and similar presentation where losing the enhancement does not remove content or actions.

Do not use sibling math to create a visual order that conflicts with DOM/keyboard order.

## Read

- [`../primitives/sibling-index-and-count.md`](../primitives/sibling-index-and-count.md)
- [`../primitives/responsive-grid-auto-fit.md`](../primitives/responsive-grid-auto-fit.md)
- [`../primitives/prefers-reduced-motion.md`](../primitives/prefers-reduced-motion.md)
