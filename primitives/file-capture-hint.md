# File `capture` Hint

**Role:** hint that a mobile file input should offer direct camera/microphone capture without a custom media-capture UI.

```html
<input
  type="file"
  name="photo"
  accept="image/*"
  capture="environment">
```

Common values:

- `user` — user-facing camera/microphone;
- `environment` — outward-facing camera/microphone.

## Compatibility

MDN marks `capture` as Limited Availability. Treat it as an optional mobile hint on top of a normal file input, never as the only upload path.

The baseline remains:

```html
<input type="file" accept="image/*">
```

## Security / validation

`capture` and `accept` are client hints. The server must still validate the uploaded content.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/capture
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input/file
