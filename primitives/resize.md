# CSS `resize`

**Role:** expose browser-owned resizing handles instead of implementing drag-resize JavaScript.

```css
.notes {
  resize: vertical;
  overflow: auto;
  min-block-size: 8rem;
  max-block-size: 60dvh;
}
```

Possible directions include:

- `horizontal`
- `vertical`
- `both`
- newer logical-axis values such as `block` / `inline` where supported

## What this replaces

```text
pointerdown
 -> pointermove
 -> calculate width/height
 -> set inline styles
 -> pointerup
```

for simple user-resizable editors/panels.

## Limitations

`resize` is not Baseline across every browser and does not apply to every box. Non-`textarea` elements generally need a non-`visible`/non-`clip` overflow mode.

Treat it as an optional ergonomic capability unless your browser matrix explicitly guarantees it.

Do not use it when product behavior requires synchronized pane ratios, persistence, snap points or complex drag affordances.

## Source

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/resize
