# Media State Pseudo-Classes

**Role:** expose `<audio>` / `<video>` playback state directly to CSS instead of mirroring media events into classes.

Newer Firefox supports selectors including:

```css
video:playing { ... }
video:paused { ... }
video:buffering { ... }
video:seeking { ... }
video:stalled { ... }
video:muted { ... }
video:volume-locked { ... }
```

## What this can replace

```text
play/pause/waiting/seeking/volume event listeners
 -> toggle .is-playing / .is-buffering / .is-muted
 -> CSS
```

when the state is needed only for presentation.

## Compatibility

Firefox shipped the media-state pseudo-classes in **Firefox 150**.

Therefore they are **not** available in PureDesign's Tor Browser 15 / Firefox 140 ESR conservative baseline.

Use as progressive presentation only. The actual media must remain usable through native [`controls`](native-media-controls.md) or another baseline path.

## Sources

- https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/150
- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/Pseudo-classes
