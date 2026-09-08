# CSS Anchor Positioning

**Role:** position floating UI relative to another element without measuring coordinates in JavaScript.

Representative shape:

```css
.trigger { anchor-name: --trigger; }

.menu {
  position: absolute;
  position-anchor: --trigger;
  position-area: block-end span-inline-end;
}
```

Fallback/flip logic can use `@position-try` in supporting browsers.

## Replaces

```text
getBoundingClientRect()
 -> calculate x/y
 -> listen for scroll/resize
 -> move overlay
```

## Rule

For Tor Browser / Firefox 140 ESR targets this is enhancement-only. Keep a conventional absolute-positioning fallback.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_anchor_positioning
- https://github.com/johannesmutter/anchorpop
- https://gist.github.com/blackspike
- https://gist.github.com/TingRubato/5a8474ed70eae1075f4db90211d510d2
