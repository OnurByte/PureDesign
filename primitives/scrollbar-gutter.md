# `scrollbar-gutter`

**Role:** Stable layout-stability primitive.

`scrollbar-gutter: stable` reserves space for classic scrollbars so content does not shift horizontally when a scrollbar appears or disappears.

```css
html {
    scrollbar-gutter: stable;
}
```

For symmetric layouts:

```css
.panel {
    overflow: auto;
    scrollbar-gutter: stable both-edges;
}
```

## Why this belongs in PureDesign

Modal/dialog transitions, expanding content, validation messages, and server-rendered page changes can change whether the page overflows. Developers often compensate for scrollbar width with JavaScript measurements and padding writes.

For the common layout-shift case, the browser can reserve the gutter itself.

## Limits

- It affects classic scrollbars; overlay scrollbars do not consume a gutter.
- It is layout stabilization, not scroll locking.
- Test modal behavior in the actual target browser because top-layer/modal handling can interact with viewport scrolling differently.

## Compatibility

MDN marks `scrollbar-gutter` as Baseline 2024. It is appropriate as stable progressive layout polish for a Firefox 140-class engine.

## Sources

- MDN: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/scrollbar-gutter
- MDN overflow guide: https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Styling_basics/Overflow
