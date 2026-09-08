# `color-scheme`

**Role:** tell the browser which color schemes native controls and browser-provided UI should use.

```css
:root {
  color-scheme: light dark;
}
```

A temporary radio-driven theme can derive this state through `:has()`:

```css
:root:has(input[name="theme"][value="light"]:checked) {
  color-scheme: light;
}

:root:has(input[name="theme"][value="dark"]:checked) {
  color-scheme: dark;
}
```

For persistent user preference, render the authoritative theme from the server and let CSS select the matching scheme.

## Source

- https://developer.mozilla.org/en-US/docs/Web/CSS/color-scheme
