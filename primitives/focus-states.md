# `:focus-visible` and `:focus-within`

**Role:** browser-owned focus state exposed to CSS.

Use `:focus-visible` for focus indication that follows the browser's input-modality heuristics:

```css
.button:focus-visible {
  outline: 2px solid var(--focus);
  outline-offset: 2px;
}
```

Use `:focus-within` when a container should react while any descendant owns focus:

```css
.field:focus-within {
  border-color: var(--accent);
}
```

`:has(input:focus-visible)` can provide a more specific derived-parent variant when needed.

## Replaces

Many scripts that only toggle `.focused` or track whether keyboard focus entered a component.

## Rule

Never remove focus outlines without providing an equally visible replacement.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/:focus-visible
- https://developer.mozilla.org/en-US/docs/Web/CSS/:focus-within
