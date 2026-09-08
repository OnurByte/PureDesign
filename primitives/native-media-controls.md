# Native `<video>` / `<audio>` Controls

**Role:** browser-owned playback UI instead of a JavaScript media-control layer.

```html
<video
  controls
  playsinline
  preload="metadata"
  poster="/media/poster.jpg"
  width="1280"
  height="720">
  <source src="/media/video.webm" type="video/webm">
  <source src="/media/video.mp4" type="video/mp4">
  <track
    default
    kind="captions"
    srclang="en"
    label="English"
    src="/media/captions-en.vtt">

  <a href="/media/video.mp4">Download the video</a>
</video>
```

With `controls`, the user agent owns normal playback interaction such as play/pause, seeking, volume and its platform-appropriate media UI. Declarative `<track>` elements add WebVTT captions/subtitles to the native control system.

## Why

Do not build custom playback controls merely to make the player look branded. Native controls preserve browser/device behavior and remain useful with client-side JavaScript completely disabled.

## Boundary

Custom streaming protocols, DRM, synchronized application state, bespoke timeline UI, analytics or other advanced media behavior may require a client runtime. Keep a directly playable native source/download route as the baseline when possible.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/video
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/audio
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/track
