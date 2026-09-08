# `:in-range` / `:out-of-range`

**Role:** browser-owned numeric/date range state.

```html
<input type="number" min="1" max="10" name="count">
```

```css
input:out-of-range {
  border-color: var(--danger);
}
```

The browser derives the state from `min` / `max` / `step`; no input listener is needed merely to paint range validity.

## Use with

- `number`
- `range`
- date/time input types where range constraints apply

Server validation remains authoritative.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/%3Ain-range
- https://developer.mozilla.org/en-US/docs/Web/CSS/%3Aout-of-range
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/min
