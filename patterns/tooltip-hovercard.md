# Tooltip / Hovercard

## Baseline

Do not ship critical information only inside a hover-only CSS tooltip. Keyboard and touch behavior must remain valid.

## Emerging native composition

- [`interestfor` + `popover="hint"`](../primitives/interestfor-and-hint-popover.md)
- optional [CSS Anchor Positioning](../primitives/anchor-positioning.md)
- optional [Anchored Container Queries](../primitives/anchored-container-queries.md) to restyle descendants when a position fallback becomes active
- watchlist: [native tooltip proposals](../primitives/native-tooltip-proposals.md)

```html
<button interestfor="save-help" class="save-trigger">Save</button>

<div id="save-help" popover="hint" class="save-help">
  <span class="save-help-surface">
    <span class="save-help-arrow" aria-hidden="true"></span>
    Saves the current document.
  </span>
</div>
```

In browsers with Anchor Positioning, the hovercard can be placed relative to the trigger and given fallback positions. In browsers that additionally support anchored container queries, descendant presentation such as the arrow can follow the fallback selected by the browser:

```css
.save-trigger {
  anchor-name: --save-trigger;
}

.save-help {
  position: absolute;
  position-anchor: --save-trigger;
  position-area: top;
  position-try-fallbacks: flip-block;
}

@supports (container-type: anchored) {
  .save-help {
    container-type: anchored;
  }

  @container anchored(fallback: flip-block) {
    .save-help-arrow {
      transform: rotate(180deg);
    }
  }
}
```

## Rule

For conservative browsers, keep help text accessible through normal document content, labels, descriptions or another explicit disclosure path. The emerging tooltip behavior, anchor placement and fallback-aware styling are enhancement-only.
