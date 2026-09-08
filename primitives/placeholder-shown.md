# `:placeholder-shown`

**Role:** browser-owned empty/placeholder presentation state.

```css
.field:has(input:placeholder-shown) .clear-affordance {
  visibility: hidden;
}
```

A common use is floating-label presentation, but keep a real `<label>` in the document. A placeholder is not a replacement for a label.

## Replaces

Visual-only code that reads `input.value` merely to toggle `.empty` / `.filled` classes.

## Caveats

- It only matches while placeholder text is actually being displayed.
- Autofill can create states that naive floating-label implementations forget to test.
- Do not encode durable application state through it.

## Community

A small 2026 Float Label CSS project uses `:has(*:placeholder-shown:not(:focus))` to build classless floating labels.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/Pseudo-classes
- https://www.reddit.com/r/css/comments/1sas5xb/
- https://github.com/anydigital/float-label-css
