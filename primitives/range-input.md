# `<input type="range">`

**Role:** browser-owned slider interaction.

```html
<label for="quality">Quality</label>
<input
  id="quality"
  type="range"
  name="quality"
  min="1"
  max="10"
  step="1"
  value="5">
```

The browser owns pointer, touch, keyboard and platform-specific slider behavior. `min`, `max` and `step` define the numeric domain; `accent-color` can provide lightweight branding.

## Boundary

A static zero-JS page cannot continuously mirror the current slider value into arbitrary text elsewhere. If live calculated output is required, that is a separate behavior requirement rather than a reason to rebuild the slider itself.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input/range
- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/accent-color
