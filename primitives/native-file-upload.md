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
- [`webkitdirectory`](directory-file-input.md) — conditional native directory selection;
- platform-native picker UI.

`accept`, `capture`, filenames and directory metadata are client input. The server must verify actual file type/content, authorization, limits and path safety.

## Directory uploads

For a complete no-JS composition, see [directory upload form](../patterns/directory-upload-form.md).

Do not assume directory hierarchy survives ordinary multipart submission just because the browser DOM exposes `File.webkitRelativePath`; verify the target browser and server parser when preserving folders is required.

## Boundary

Without client-side JavaScript you do not get local previews before submission, custom drag/drop orchestration, chunked uploads, or live upload progress. Keep the ordinary multipart endpoint as the reliable baseline even when another client exists.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input/file
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/multiple
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/accept
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/capture
- https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement/webkitdirectory
