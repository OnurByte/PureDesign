# `overscroll-behavior`

**Role:** Conditional scroll-interaction primitive. Verify the exact browser matrix.

Nested scroll areas normally chain scrolling to their ancestors when they hit an edge. `overscroll-behavior` can contain that interaction without wheel/touch event handlers.

```css
.drawer-body,
.bottom-sheet,
.command-palette-results {
    overflow: auto;
    overscroll-behavior: contain;
}
```

## Replaces

Some uses of event listeners whose only job is preventing scroll chaining or browser edge gestures:

```text
wheel/touchmove listener
 -> detect scroll boundary
 -> preventDefault()
```

## Values

- `auto` — normal browser behavior
- `contain` — keep overscroll effects inside the element but stop scroll chaining to ancestors
- `none` — stop chaining and suppress default overscroll effects

Prefer `contain` unless you have a strong reason to suppress browser behavior more aggressively.

## Important side effects

`contain`/`none` may affect browser navigation gestures and pull-to-refresh behavior. Do not apply them globally as a generic reset.

Use them narrowly on scroll areas where chaining is actually harmful.

## Sources

- MDN property: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/overscroll-behavior
- MDN guide: https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Overscroll_behavior
