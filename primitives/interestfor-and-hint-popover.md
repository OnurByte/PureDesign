# `interestfor` + `popover="hint"`

**Role:** emerging declarative tooltip/hovercard interest state.

```html
<button interestfor="save-help">Save</button>

<div id="save-help" popover="hint">
  Saves the current document.
</div>
```

The direction is to let the user agent handle interest across pointer, keyboard and touch rather than implementing a `:hover`-only tooltip.

## Popover mode semantics

```text
auto   -> light-dismiss menu/panel stack
hint   -> lightweight hint stack
manual -> explicit control only
```

Popover mode is state semantics, not merely styling.

## Status

Future-watchlist / enhancement only for Firefox ESR/Tor targets.

## Sources

- https://developer.chrome.com/blog/new-in-chrome-142
- https://github.com/whatwg/html/issues/10309
- https://github.com/MicrosoftEdge/MSEdgeExplainers/blob/main/CSSTooltipPseudo/explainer.md
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes/popover
