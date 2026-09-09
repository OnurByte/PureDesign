# `:dir()`

**Role:** style elements from their browser-determined text direction without `.rtl` / `.ltr` class injection.

```css
.message:dir(rtl) {
  text-align: start;
}

.message:dir(ltr) {
  text-align: start;
}
```

More useful differences may involve icons or directional decoration:

```css
.breadcrumb-separator:dir(rtl) {
  transform: scaleX(-1);
}
```

`:dir()` follows the element's computed directionality rather than merely checking whether a `dir` attribute is physically present on that exact element.

## Compose

- [`dir="auto"`](dir-auto.md) for unknown user-generated text.
- [`<bdi>`](bdi.md) for inline isolation.
- [logical properties](logical-properties.md) so most geometry needs no direction-specific branch at all.

## Rule

Use `:dir()` only for the small remaining presentation differences that truly depend on direction. Prefer logical properties for ordinary spacing/positioning.

## Source

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/:dir
