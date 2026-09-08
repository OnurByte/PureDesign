# Bottom Sheet as a Scrolling System

## Compose

- [CSS Scroll Snap](../primitives/scroll-snap.md)

## Idea

Instead of reproducing touch physics with pointer events, velocity calculations and transforms, model the sheet as a scroll container with snap positions.

```css
.bottom-sheet {
  overflow-y: auto;
  scroll-snap-type: y mandatory;
}

.bottom-sheet__snap {
  scroll-snap-align: start;
}
```

## Why

The browser already owns momentum, scroll physics and snapping.

```text
pointermove + rAF + velocity + translateY
                ↓
         browser scrolling
```

## Source idea

- https://github.com/viliket/pure-web-bottom-sheet
- https://www.reddit.com/r/css/comments/1on7rhn/

Treat the repository as an architectural experiment; validate accessibility and actual mobile ergonomics for your product.
