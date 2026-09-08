# Theme Switcher

## System-following theme with no interaction state

If the product simply follows the browser/OS scheme, keep the browser authoritative:

```css
:root {
  color-scheme: light dark;
  --surface: light-dark(#fff, #111214);
  --text: light-dark(#15171b, #f4f5f6);
}
```

For browsers/architectures where explicit media blocks are preferable, use [`prefers-color-scheme`](../primitives/prefers-color-scheme.md).

This avoids JavaScript theme detection and keeps native controls aligned with the document scheme.

## Temporary local state

If the page needs an immediate non-persistent Light/System/Dark selector, use real radio controls and derive presentation with `:has()`:

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

Do not require localStorage JavaScript for the theme to work.

## Compose

- [native selection state](../primitives/form-selection-state.md)
- [`:has()`](../primitives/has.md)
- [`prefers-color-scheme`](../primitives/prefers-color-scheme.md)
- [`color-scheme`](../primitives/color-scheme.md)
- [`light-dark()`](../primitives/light-dark.md)
- [server-authoritative state](../principles/server-authoritative-state.md)
