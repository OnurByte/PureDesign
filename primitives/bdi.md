# `<bdi>` — Bidirectional Isolation

**Role:** isolate unknown-direction inline text so it cannot corrupt surrounding punctuation/order.

```html
<p>Owner: <bdi>{{ username }}</bdi></p>
```

Use when embedded user/database text can be LTR or RTL and should determine its own direction independently of surrounding text.

`<bdi>` behaves as if direction is inferred from its own contents while isolating that directionality from the surrounding paragraph.

## Why

Do not run language/direction detection JavaScript merely to safely print usernames, filenames or other unknown-direction inline values.

If a semantic block/element already exists, prefer putting `dir="auto"` on that element rather than wrapping everything in `<bdi>`.

## Source

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/bdi
