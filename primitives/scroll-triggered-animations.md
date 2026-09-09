# Scroll-Triggered Animations

**Role:** start, pause, reset or replay a normal time-based CSS animation when a scroll condition is crossed, without an `IntersectionObserver` or scroll listener.

Scroll-triggered animations are different from [scroll-driven animations](scroll-driven-animations.md):

```text
scroll-driven   -> scrolling directly controls animation progress
scroll-triggered -> scrolling starts/changes a time-based animation
```

Representative shape:

```css
.card {
  animation: reveal .35s ease-out both paused;
  animation-trigger: --reveal play-forwards;
}

.cards {
  timeline-trigger: --reveal view() cover;
}
```

Exact trigger syntax is still new; verify current browser documentation before shipping.

## Good uses

- reveal/fade polish as an item enters view;
- start a decorative emphasis animation once a threshold is crossed;
- reset/replay presentation when an element leaves and re-enters a range.

## Rule

The element must remain readable and usable when no animation runs.

Do not use opacity/transform initialization that permanently hides content in an unsupported browser. Treat the trigger as decoration only and respect motion preferences:

```css
@media (prefers-reduced-motion: no-preference) {
  /* progressive trigger declarations */
}
```

## Compatibility

Chrome and Edge 146 shipped scroll-triggered animations. This is **not** core for Firefox 140 ESR / Tor Browser, and Firefox/Safari do not currently provide the required conservative baseline.

Never make task completion depend on `animation-trigger`.

## Sources

- https://developer.chrome.com/release-notes/146
- https://developer.chrome.com/blog/scroll-triggered-animations
- https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animations
