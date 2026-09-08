# `text-overflow`

**Role:** visually truncate overflowing single-line labels without measuring string width in JavaScript.

```css
.filename {
  min-inline-size: 0;
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
```

This is useful for filenames, breadcrumbs, table cells and compact card metadata.

## Important

`text-overflow` only controls presentation; the actual text remains in the DOM. Preserve a way to access the full value when it is important, for example through the containing link/detail view or adjacent metadata.

Do not truncate server data merely to match the visual clipping.

`text-overflow` handles inline-direction overflow. Multi-line clamping is a different, less interoperable feature.

## Source

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/text-overflow
