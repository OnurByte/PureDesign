# CSS Math for Responsive Sizing (`min()` / `max()` / `clamp()`)

**Role:** express bounded responsive sizes directly in layout rather than recalculating them in resize JavaScript.

```css
.page {
  inline-size: min(100% - 2rem, 72rem);
}

.title {
  font-size: clamp(1.25rem, 1rem + 2vw, 2.5rem);
}
```

The browser continuously resolves mixed units such as viewport units, percentages and fixed bounds.

## Replaces

```text
resize listener
 -> calculate width/font size
 -> clamp in JS
 -> write inline style
```

when the calculation is purely presentational.

## Accessibility

Avoid fluid typography formulas that effectively prevent user zoom or produce unreadably small/large text. Keep sensible relative-unit minimums and maximums.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/clamp
- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/min
- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/max
