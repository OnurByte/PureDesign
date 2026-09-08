# Tooltip / Hovercard

## Baseline

Do not ship critical information only inside a hover-only CSS tooltip. Keyboard and touch behavior must remain valid.

## Emerging native composition

- [`interestfor` + `popover="hint"`](../primitives/interestfor-and-hint-popover.md)
- optional [CSS Anchor Positioning](../primitives/anchor-positioning.md)
- watchlist: [native tooltip proposals](../primitives/native-tooltip-proposals.md)

```html
<button interestfor="save-help">Save</button>
<div id="save-help" popover="hint">Saves the current document.</div>
```

## Rule

For conservative browsers, keep help text accessible through normal document content, labels, descriptions or another explicit disclosure path. The emerging tooltip behavior is enhancement-only.
