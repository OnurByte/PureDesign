# Dynamic Viewport Units (`dvh` / `svh` / `lvh`)

**Role:** let CSS track mobile browser viewport behavior without `window.innerHeight` resize JavaScript.

```css
.app-shell {
  min-block-size: 100dvh;
}
```

The newer viewport families distinguish:

- `svh` — small viewport height;
- `lvh` — large viewport height;
- `dvh` — dynamic viewport height that changes with browser UI.

Equivalent width/min/max variants also exist.

## Replaces

Classic mobile workaround:

```text
read window.innerHeight
 -> set --vh custom property
 -> update on resize/orientation change
```

for layouts whose only requirement is matching the current viewport.

## Compatibility

Firefox introduced the small/large/dynamic viewport units in Firefox 101, so they are inside the Firefox 140 ESR engine baseline.

## Boundary

Choose the semantic viewport size deliberately. `dvh` can resize as browser chrome appears/disappears; for some layouts a stable `svh`/`lvh` constraint produces better UX.

## Sources

- https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/101
- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/length
