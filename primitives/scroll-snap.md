# CSS Scroll Snap

**Role:** browser-owned snapping and momentum for scroll-based UI.

```css
.track {
  display: flex;
  overflow-x: auto;
  scroll-snap-type: x mandatory;
}

.track > * {
  flex: 0 0 min(85%, 24rem);
  scroll-snap-align: start;
}
```

## Use for

- basic carousels
- horizontal card rails
- snap-based bottom-sheet experiments

## Architectural lesson

Do not recreate browser scroll physics with pointer tracking and `requestAnimationFrame` if the interaction can be represented as scrolling.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_scroll_snap
- https://github.com/viliket/pure-web-bottom-sheet
- https://github.com/demetris/omni-carousel
