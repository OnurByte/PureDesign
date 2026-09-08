# Scroll-Driven Animations

**Role:** optional visual effects tied to scroll/view timelines.

Representative syntax:

```css
.reveal {
  animation: fade-in linear both;
  animation-timeline: view();
}
```

## Rule

Treat this as decoration only. Content visibility, navigation and task completion must not depend on a scroll-driven animation running.

## Compatibility

For conservative Firefox/Tor targets this remains experimental/enhancement-only; Firefox release notes have continued to list the feature behind preferences in relevant versions.

## Source

- https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/155
