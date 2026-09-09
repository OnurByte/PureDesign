# Scroll-Driven Animations

**Role:** optional visual effects whose progress is directly tied to scroll/view timelines.

Representative syntax:

```css
.reveal {
  animation: fade-in linear both;
  animation-timeline: view();
}
```

## Distinguish from scroll-triggered animation

```text
scroll-driven    -> scroll position directly controls animation progress
scroll-triggered -> crossing a scroll condition starts/changes a normal time-based animation
```

For the second case, read [scroll-triggered animations](scroll-triggered-animations.md). Do not reach for a scroll listener or `IntersectionObserver` merely because the effect needs a one-time trigger in browsers that support the newer declarative primitive.

## Rule

Treat both forms as decoration only. Content visibility, navigation and task completion must not depend on an animation running.

Respect `prefers-reduced-motion`, and make the unsupported-browser state fully readable.

## Compatibility

For conservative Firefox/Tor targets scroll-driven animation remains enhancement-only; Firefox release notes have continued to list relevant support behind preferences in newer versions. Scroll-triggered animations are even newer and are tracked separately.

## Sources

- https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/155
- https://developer.chrome.com/release-notes/146
