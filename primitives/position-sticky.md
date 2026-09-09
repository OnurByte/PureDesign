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
 -> recalculate width/left
```

for ordinary sticky headers, table headers, sidebars and action bars.

## Footguns

- At least one inset on the sticky axis must be non-`auto`.
- The nearest ancestor with a scrolling mechanism influences where it sticks.
- Parent `overflow` choices can create an unexpected scroll container and change/break the intended sticky behavior.
- Sticky/fixed content can obscure other content at high zoom; test real accessibility scenarios.
- Sticky elements may cause repaints during scrolling; keep expensive effects restrained.
- Sticky positioning and **styling based on whether the element is currently stuck** are different problems. For the latter, see [scroll-state container queries](scroll-state-container-queries.md) as a newer enhancement.

## Real-world failure case

A design-system issue documents a sticky table header failing because the parent table wrapper used `overflow-x: auto`; this is a useful reminder that sticky belongs to the scroll-layout model, not an isolated declaration:

- https://github.com/ithaka/pharos/issues/820

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/position
- Community discussion comparing sticky with scroll JavaScript: https://www.reddit.com/r/webdev/comments/14mcy7j/
