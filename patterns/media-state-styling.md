# Media State Styling Without Event-to-Class JavaScript

## Baseline

Keep media usable with native controls:

```html
<video controls preload="metadata">
  <source src="/media/video.webm" type="video/webm">
</video>
```

See [`native-media-controls.md`](../primitives/native-media-controls.md).

## Newer progressive styling

In browsers supporting [media state pseudo-classes](../primitives/media-state-pseudo-classes.md):

```css
video:buffering {
  outline: 2px dashed currentColor;
}

video:paused {
  opacity: .95;
}

video:playing {
  outline-color: transparent;
}
```

This removes presentation-only listeners such as:

```text
play -> add .playing
pause -> add .paused
waiting -> add .buffering
volumechange -> add .muted
```

## Compatibility

Firefox ships these selectors in Firefox 150, so they are not Tor Browser 15 / Firefox 140 ESR core.

Unsupported browsers should simply lose the extra state styling; playback remains available through native controls.
