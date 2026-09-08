# `prefers-color-scheme`

**Role:** read the user's system/browser light/dark preference directly in CSS.

```css
:root {
  color-scheme: light dark;
}

@media (prefers-color-scheme: dark) {
  :root {
    --surface: #111;
    --text: #eee;
  }
}
```

The preference comes from the operating system or browser. No `matchMedia()` JavaScript is required for presentation.

## Related

- [`color-scheme`](color-scheme.md) tells the browser which schemes native UI can render in.
- [`light-dark()`](light-dark.md) can select values without repeating media-query blocks in supporting browsers.
- Persistent explicit user overrides still belong in server/cookie/account state when the product offers them.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/%40media/prefers-color-scheme
- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/color-scheme
