# `reading-flow` and `reading-order`

**Role:** Experimental/progressive accessibility enhancement. Do not make core behavior depend on it yet.

Responsive Grid/Flex layouts can visually reorder controls while DOM, screen-reader, and sequential keyboard order remain different. `reading-flow` is an emerging CSS mechanism for aligning reading/tab order with intended visual flow without rewriting or duplicating the DOM.

```css
.dashboard-grid {
    display: grid;
    grid-template-columns: 1fr 2fr;
    reading-flow: grid-rows;
}
```

For more explicit ordering, a reading-flow container can use `reading-order` on children.

## Replaces a bad class of workarounds

Without a platform primitive, developers sometimes:

- duplicate markup for different breakpoints
- manipulate DOM order with JavaScript
- use positive `tabindex` values
- accept a mismatch between visual and keyboard order

Those approaches can create accessibility and maintenance problems.

## Rule

**Good DOM source order remains the baseline.** Do not deliberately write nonsensical source order because `reading-flow` exists.

Use this only when a legitimate responsive layout causes visual and sequential-navigation order to diverge and the target browsers support the feature.

## Current status

MDN marks `reading-flow` as experimental / Limited Availability in 2026. It is not a Tor Browser 15 / Firefox 140 ESR core primitive.

## Sources

- MDN `reading-flow`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/reading-flow
- MDN `reading-order`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/reading-order
