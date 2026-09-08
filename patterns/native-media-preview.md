# Native Media Preview

## Compose

- [native media controls](../primitives/native-media-controls.md)
- normal server authorization/download routes

For a file manager or storage application, a preview does not need a JavaScript player if the browser can play the media directly:

```html
<figure>
  <video controls preload="metadata" src="/files/42/content"></video>
  <figcaption>demo.mp4</figcaption>
</figure>
```

Audio is the same idea:

```html
<audio controls src="/files/77/content">
  <a href="/files/77/download">Download audio</a>
</audio>
```

## Server contract

The media endpoint must provide the correct content type and should support HTTP byte ranges when seeking/large media requires it.

## Rule

Prefer the native player for ordinary preview/playback. Add a custom media runtime only when the product requirement genuinely exceeds what the browser player supplies.
