# Mobile App Shell Without Viewport JavaScript

## Compose

- [dynamic viewport units](../primitives/dynamic-viewport-units.md)
- [safe-area environment variables](../primitives/safe-area-env.md)
- [`position: sticky`](../primitives/position-sticky.md)
- [overscroll behavior](../primitives/overscroll-behavior.md) only where necessary

```css
.app {
  min-block-size: 100dvh;
  display: grid;
  grid-template-rows: auto 1fr auto;
}

.app__footer {
  position: sticky;
  inset-block-end: 0;
  padding-block-end: calc(.75rem + env(safe-area-inset-bottom));
}
```

## Avoid

```text
window.innerHeight
resize listener
UA sniff for iPhone notch
fixed pixel safe-area tables
```

The browser knows the viewport and system-safe area. Describe the desired layout instead of synchronizing those measurements into CSS with JavaScript.
