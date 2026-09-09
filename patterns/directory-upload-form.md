# Directory Upload Form

Use the browser's file picker and an ordinary multipart form when a user should be able to upload a folder without client-side JavaScript.

## Compose

- [native file upload](../primitives/native-file-upload.md)
- [directory file input](../primitives/directory-file-input.md)
- [`::file-selector-button`](../primitives/file-selector-button.md) for optional styling

## Baseline

Keep normal file upload available even when directory selection is offered:

```html
<form action="/uploads" method="post" enctype="multipart/form-data">
  <fieldset>
    <legend>Upload files</legend>

    <label for="files">Choose files</label>
    <input id="files" type="file" name="files[]" multiple>
  </fieldset>

  <fieldset>
    <legend>Upload a folder</legend>

    <label for="folder">Choose folder</label>
    <input
      id="folder"
      type="file"
      name="folder_files[]"
      webkitdirectory
      multiple>
  </fieldset>

  <button type="submit">Upload</button>
</form>
```

The browser owns picker interaction and multipart submission. No drop-zone runtime or filesystem traversal code is required in the page.

## Server contract

The server remains authoritative. It must validate every received file independently of picker hints.

If the product needs to recreate the selected directory hierarchy, first verify that the target browser and multipart parser preserve usable relative-path information. Do not promise hierarchy preservation merely because `File.webkitRelativePath` exists in the browser DOM API.

Treat any received path-like filename as hostile input:

```text
normalize
-> reject absolute/traversal paths
-> enforce destination root
-> resolve collisions
-> validate file count/size/content
-> write only after authorization
```

## Empty directories

A directory picker selects files. Empty directories have no file entry and therefore cannot be faithfully reconstructed through this pattern.

## What this does not provide

Without browser-side JavaScript this pattern does not provide:

- a custom drag-and-drop zone;
- pre-upload file-tree rendering;
- per-file client progress;
- resumable/chunk orchestration;
- client-side conflict resolution.

Those features need another client or server/request architecture. Do not smuggle a JS uploader into the pattern.

## Compatibility

The ordinary file-upload field is the reliable baseline. `webkitdirectory` is a conditional native enhancement: broad browser support, but still non-standard and worth testing in the actual Tor/browser/server stack.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input/file
- https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement/webkitdirectory
- https://developer.mozilla.org/en-US/docs/Web/API/File/webkitRelativePath
