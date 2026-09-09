# Native Media Preview

## Compose

- [native media controls](../primitives/native-media-controls.md)
- optional newer [media state pseudo-classes](../primitives/media-state-pseudo-classes.md) for presentation-only state styling
- normal server authorization/download routes

For a file manager or storage application, a preview does not need a JavaScript player if the browser can play the media directly:

```html
<figure>
  <video controls preload="metadata" src="/files/42/content"></video>
  <figcaption>demo.mp4</figcaption>
</figure>
```

Audio uses the same baseline:

```html
<audio controls src="/files/77/content">
  <a href="/files/77/download">Download audio</a>
</audio>
```

Captions/subtitles can use native `<track>` / WebVTT where appropriate.

## Server contract

The media endpoint must:

- authorize access on the server;
- return the correct media `Content-Type`;
- support HTTP byte ranges when seeking/large-media playback requires it;
- provide a normal download URL when download is a supported action.

## Progressive state styling

Firefox 150+ can expose playback states such as `:playing`, `:paused` and `:buffering` directly to CSS. See [`media-state-styling.md`](media-state-styling.md).

Those selectors are enhancement only for the Tor Browser / Firefox 140 ESR target; native playback remains the baseline.

## Rule

Prefer the native player for ordinary preview/playback. Add a custom media runtime only when the product requirement genuinely exceeds what the browser player supplies, such as application-specific timelines/editing/DRM/streaming logic.
