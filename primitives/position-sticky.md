# `position: sticky`

**Role:** browser-owned sticky positioning instead of scroll listeners that manually toggle `fixed` state.

```css
.toolbar {
  position: sticky;
  inset-block-start: 0;
  z-index: 10;
}
```

The element participates in normal flow until its scroll container reaches the configured inset, then the browser keeps it at that threshold.

## Replaces

```text
scroll listener
 -> getBoundingClientRect()
 -> compare top
 -> toggle position: fixed / class
```

for ordinary sticky headers, sidebars and action bars.

## Footguns

- At least one inset on the sticky axis must be non-`auto`.
- The nearest ancestor with a scrolling mechanism influences where it sticks.
- Sticky behavior and **styling based on whether it is currently stuck** are different problems. For the latter, see [scroll-state container queries](scroll-state-container-queries.md) as a newer enhancement.

## Source

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/position
