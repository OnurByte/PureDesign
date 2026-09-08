# Safe-Area Environment Variables

**Role:** place fixed/sticky application UI around notches, rounded displays and browser/OS occupied areas without device-model detection.

```css
.bottom-bar {
  position: sticky;
  inset-block-end: 0;
  padding:
    .75rem
    calc(1rem + env(safe-area-inset-right))
    calc(.75rem + env(safe-area-inset-bottom))
    calc(1rem + env(safe-area-inset-left));
}
```

The user agent supplies `safe-area-inset-top/right/bottom/left`. On unobstructed rectangular viewports these are normally zero.

## Replaces

- iPhone/notch model detection;
- hard-coded device padding tables;
- JS measurements used only to avoid system UI overlap.

## Boundary

Environment-variable families are growing (foldable viewport segments, titlebar areas, keyboards). Do not assume every newer environment variable is supported just because `env()` itself is mature.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/env
- https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Environment_variables/Using
