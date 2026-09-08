# Native File Upload

**Role:** browser file picker + ordinary multipart form submission.

```html
<form action="/files" method="post" enctype="multipart/form-data">
  <label for="uploads">Choose files</label>
  <input
    id="uploads"
    type="file"
    name="uploads[]"
    accept="image/*,.pdf"
    multiple>

  <button type="submit">Upload</button>
</form>
```

The browser owns file selection and multipart encoding.

## Available native hints

- `multiple` — select multiple files;
- `accept` — hint accepted MIME types/extensions;
- [`capture`](file-capture-hint.md) — optional mobile camera/microphone hint with Limited Availability;
- platform-native picker UI.

`accept` and `capture` are only client hints. The server must verify actual file type/content.

## Boundary

Without client-side JavaScript you do not get local previews, drag/drop orchestration, chunked uploads, or live upload progress. Keep the ordinary multipart endpoint as the reliable baseline even when another client exists.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input/file
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/multiple
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/accept
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/capture
