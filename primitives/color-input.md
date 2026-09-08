# `<input type="color">`

**Role:** browser/OS-owned color picker instead of a JavaScript color-picker dependency.

```html
<label>
  Accent color
  <input type="color" name="accent" value="#7c3aed">
</label>
```

The control UI varies substantially by browser/platform, but the browser owns the picker interaction and form value.

## Newer capabilities

Modern HTML is expanding color inputs with richer CSS color values plus `alpha` and `colorspace` hints. Treat those additions as separately compatibility-sensitive; the basic color picker is the conservative baseline.

## Boundary

Use a custom picker only when the product genuinely requires capabilities the native picker cannot supply. Visual consistency alone is usually not enough reason to replace platform interaction.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input/color
