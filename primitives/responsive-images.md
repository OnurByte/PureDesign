# Responsive Images: `<picture>` / `srcset` / `sizes`

**Role:** image source selection owned by the browser instead of viewport/device JavaScript.

Art direction / format selection:

```html
<picture>
  <source media="(width < 40rem)" srcset="/img/card-mobile.avif" type="image/avif">
  <source srcset="/img/card.avif" type="image/avif">
  <img src="/img/card.jpg" alt="File preview" width="1200" height="800">
</picture>
```

Density/width candidates can also use `srcset` and `sizes` on `<img>`.

## Replaces

- `window.innerWidth` image-source switching;
- device-pixel-ratio source scripts;
- format-detection JavaScript for common image formats.

The browser can consider media conditions, supported formats, density and data-saving behavior.

Always provide meaningful `alt` text and intrinsic `width`/`height` where known.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/picture
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/img
