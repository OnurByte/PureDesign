# Modern Typed `attr()`

**Role:** consume HTML attribute values directly in CSS properties without reading `dataset` in JavaScript.

```html
<div class="bar" data-size="72"></div>
```

```css
@supports (width: attr(data-size type(<number>))) {
  .bar {
    width: calc(attr(data-size type(<number>)) * 1%);
  }
}
```

Modern `attr()` syntax supports types/units and fallbacks, allowing server-rendered metadata to feed CSS values directly.

## Compatibility

Firefox 155 expanded `attr()` to any CSS property. MDN still notes that non-`content` usage has varying/experimental support across the ecosystem.

This is far newer than Firefox 140 ESR. Always provide a baseline declaration before the enhanced one.

## Security / architecture boundary

`data-*` is presentation input, not trusted application authority. Do not encode permissions or security decisions in CSS attributes.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/attr
- https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/155
