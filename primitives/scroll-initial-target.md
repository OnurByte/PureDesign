# `scroll-initial-target`

**Role:** declaratively choose an element as the initial snap target of a scroll container.

```css
.gallery {
  overflow-x: auto;
  scroll-snap-type: x mandatory;
}

.gallery > * {
  scroll-snap-align: center;
}

.gallery > .is-current {
  scroll-initial-target: nearest;
}
```

The server can render `.is-current` from durable state. Supporting browsers can then start the scroller near that item without imperative scrolling code.

## Boundary

This is initial presentation state, not durable application state. The server/URL still owns which item is current.

Fragment navigation has stronger navigation semantics and should remain the baseline when the user must be able to link/bookmark a target.

## Compatibility

This property is experimental/limited. Chromium shipped it from Chrome 133; current Firefox does not provide normal release support. It is **not** available for the Firefox 140/Tor baseline.

Use only as progressive enhancement around a scroller that is fully usable from its normal starting position.

## Sources

- MDN: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/scroll-initial-target
- Explainer: https://github.com/DavMila/explainer-scroll-initial-target
- CSS Scroll Snap Level 2: https://drafts.csswg.org/css-scroll-snap-2/#scroll-initial-target
