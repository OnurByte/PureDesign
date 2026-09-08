# Native Download Links

**Role:** use normal navigation/download semantics instead of `fetch() -> Blob -> objectURL -> click()` glue JavaScript.

```html
<a href="/files/42/download" download="report.pdf">
  Download report
</a>
```

For same-origin resources, the `download` attribute can suggest download behavior and a filename. Server response headers such as `Content-Disposition` remain the authoritative/reliable way to define download handling.

## Why

If the server already exposes a download endpoint, a normal anchor is usually the complete client.

```text
click
 -> HTTP GET
 -> server authorization
 -> response body
 -> browser download UI
```

No client fetch or Blob buffering is necessary.

## Boundary

The attribute has cross-origin/browser restrictions and must not be treated as a security control. Authorization and filenames still need safe server handling.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/a#download
