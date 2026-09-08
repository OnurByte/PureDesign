# Theme Switcher

## Temporary local state

Use real radio controls and derive presentation with `:has()`:

```html
<label><input type="radio" name="theme" value="system" checked> System</label>
<label><input type="radio" name="theme" value="light"> Light</label>
<label><input type="radio" name="theme" value="dark"> Dark</label>
```

```css
:root:has(input[name="theme"][value="light"]:checked) {
  color-scheme: light;
}

:root:has(input[name="theme"][value="dark"]:checked) {
  color-scheme: dark;
}
```

## Persistent preference

Persist on the server/cookie/account and render the authoritative state:

```html
<html data-theme="dark">
```

## Compose

- [native selection state](../primitives/form-selection-state.md)
- [`:has()`](../primitives/has.md)
- [`color-scheme`](../primitives/color-scheme.md)
- [server-authoritative state](../principles/server-authoritative-state.md)

Do not require localStorage JavaScript for the theme to work.
