# RTL-Safe Component Layout

## Compose

- [`dir="auto"`](../primitives/dir-auto.md) for unknown-direction content
- [`<bdi>`](../primitives/bdi.md) for isolated inline user values
- [CSS logical properties](../primitives/logical-properties.md) for geometry

## Example

```html
<article class="file-row">
  <span class="file-name" dir="auto">{{ filename }}</span>
  <span class="file-size">{{ size }}</span>
  <a class="file-action" href="{{ downloadUrl }}">Download</a>
</article>
```

```css
.file-row {
  display: flex;
  gap: .75rem;
  padding-inline: 1rem;
}

.file-action {
  margin-inline-start: auto;
}
```

Do not branch:

```text
if rtl => margin-left
else    => margin-right
```

when the intent is simply “put this at inline end.”

## Rule

Directionality belongs to HTML/content. Geometry should usually be flow-relative CSS.

For an entire known-locale page, set the document's real `dir`. For arbitrary filenames/usernames/messages, isolate or auto-detect only the content that is actually unknown-direction.
