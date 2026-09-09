# Directory File Input (`webkitdirectory`)

**Role:** let the browser present a directory picker and select the files under that directory without building a custom file-tree picker in client JavaScript.

```html
<input
  id="folder"
  type="file"
  name="files[]"
  webkitdirectory
  multiple>
```

Despite the vendor-prefixed name, `webkitdirectory` has broad modern browser support. It remains non-standard and needs product-specific testing.

## Browser-owned result

Selecting a directory produces a flat set of files. Browsers also expose relative-path metadata for selected files through `File.webkitRelativePath`.

Conceptually:

```text
Photos/
  2026/
    trip.jpg

-> selected file set contains trip.jpg
-> browser-side File metadata can describe Photos/2026/trip.jpg
```

## Important PureDesign boundary

The DOM `File.webkitRelativePath` property is useful to scripting clients, but PureDesign cannot read it with client JavaScript.

For an ordinary multipart form, **do not assume** every browser and server framework will preserve directory hierarchy in exactly the same way. Test the actual browser -> multipart parser -> application stack if preserving folders is a product requirement.

The safe contract is:

```text
folder picker      -> native enhancement
file upload        -> ordinary multipart baseline
folder reconstruction -> only after verified server-side interoperability
```

## Missing information

Empty directories do not have file entries, so a file-based directory upload cannot reliably reconstruct empty folders.

## Security

Any submitted filename or relative-path-like value is untrusted input. The server must:

- reject absolute paths;
- reject `.` / `..` traversal segments;
- normalize separators deliberately;
- enforce upload count and byte limits;
- validate actual file content/type;
- handle duplicate/colliding paths;
- authorize the destination independently of the submitted path.

Never concatenate a client-provided path directly onto a filesystem destination.

## Compatibility

Firefox has supported `webkitdirectory` since Firefox 50, so the Firefox 140 engine is old enough to expose the capability. However, because the feature is non-standard and file-system UI can differ by product/platform, classify it as **Conditional** and test the actual Tor Browser target before making folder selection essential.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input#webkitdirectory
- https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement/webkitdirectory
- https://developer.mozilla.org/en-US/docs/Web/API/File/webkitRelativePath
- https://wicg.github.io/entries-api/

## Research examples

- https://github.com/silverwind/uppie
- https://github.com/node-formidable/formidable
