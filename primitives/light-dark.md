# `light-dark()`

**Role:** Stable theme/presentation primitive for the Firefox 140 ESR baseline.

When a document opts into both schemes, `light-dark()` can select a value from the active browser color scheme without duplicating every declaration inside `prefers-color-scheme` queries.

```css
:root {
    color-scheme: light dark;

    --surface: light-dark(#ffffff, #111214);
    --text: light-dark(#16181d, #f5f6f7);
    --border: light-dark(#d9dce2, #34373d);
}

body {
    background: var(--surface);
    color: var(--text);
}
```

## Replaces

For system-following themes, repeated CSS such as:

```text
base light variables
@media (prefers-color-scheme: dark) { redefine every variable }
```

It does not replace server-owned persistence for a user-selected Light/Dark/System account preference.

## Firefox/Tor relevance

Firefox added `light-dark()` in Firefox 120, so the function predates the Firefox 140 ESR engine in Tor Browser 15.0.21.

## Rule

Use `color-scheme` so native controls, form widgets, scrollbars, and UA surfaces can also adopt the scheme. Do not merely recolor application backgrounds while leaving browser-owned controls mismatched.

## Sources

- MDN `light-dark()`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/color_value/light-dark
- MDN `color-scheme`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/color-scheme
- Firefox 120 release notes: https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/120
