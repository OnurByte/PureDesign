# Scroll Anchoring and `overflow-anchor`

**Role:** preserve the user's scroll position when layout above the viewport changes, and selectively opt elements out of being scroll anchors.

Browsers that implement scroll anchoring normally do it automatically. In most interfaces the correct rule is: **do nothing and keep the default**.

Use `overflow-anchor: none` only when a specific subtree makes the browser choose a bad anchor:

```css
.transient-banner {
  overflow-anchor: none;
}
```

## What it replaces

For layout shifts caused by late media sizing, font/render changes or inserted server-rendered content, browser scroll anchoring can remove the need for manual `scrollTop` compensation.

It is not data virtualization and it does not remove layout shifts by itself. Reserve intrinsic media dimensions and stable layout first.

## Dangerous global rule

Avoid this unless the product specifically requires it:

```css
* {
  overflow-anchor: none;
}
```

That disables a browser behavior intended to keep reading position stable.

## Compatibility

Firefox supports `overflow-anchor` from Firefox 66, so it is available in the Firefox 140 ESR baseline. Safari support is newer/uneven, therefore treat explicit opt-out styling as conditional across a broad browser matrix.

## Sources

- MDN property: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/overflow-anchor
- MDN scroll anchoring guide: https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Scroll_anchoring/Overview
- CSS Scroll Anchoring: https://drafts.csswg.org/css-scroll-anchoring/
