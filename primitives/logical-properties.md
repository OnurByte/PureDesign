# CSS Logical Properties

**Role:** make component layout follow writing direction and writing mode without JavaScript branching.

Prefer flow-relative properties:

```css
.file-row {
  padding-inline: 1rem;
  margin-block-end: .5rem;
}

.file-row__actions {
  margin-inline-start: auto;
}

.badge {
  position: absolute;
  inset-block-start: .5rem;
  inset-inline-end: .5rem;
}
```

instead of hard-coding physical directions:

```css
padding-left: 1rem;
margin-right: auto;
right: .5rem;
top: .5rem;
```

## What this replaces

```text
if RTL -> swap left/right classes
if vertical writing mode -> swap width/height assumptions
```

The browser maps `inline-start`, `inline-end`, `block-start`, and `block-end` according to `dir` and `writing-mode`.

Useful families include:

- `margin-inline` / `margin-block`
- `padding-inline` / `padding-block`
- `inset-inline` / `inset-block`
- `inline-size` / `block-size`
- logical border/radius properties
- `text-align: start/end`

## State boundary

Text direction -> HTML/content/browser.

Flow-relative geometry -> CSS.

Do not duplicate component styles into `.rtl` / `.ltr` versions when logical properties express the actual intent.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Logical_properties_and_values
- https://developer.mozilla.org/en-US/docs/Glossary/Logical_properties
- https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Logical_properties_and_values/Floating_and_positioning
