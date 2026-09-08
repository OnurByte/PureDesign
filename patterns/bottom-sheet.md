# Bottom Sheet as a Scrolling System

## Compose

- [CSS Scroll Snap](../primitives/scroll-snap.md)
- optional [overscroll containment](../primitives/overscroll-behavior.md)

## Idea

Instead of reproducing touch physics with pointer events, velocity calculations and transforms, model the sheet as a scroll container with snap positions.

```css
.bottom-sheet {
  overflow-y: auto;
  scroll-snap-type: y mandatory;
  overscroll-behavior-y: contain;
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

`overscroll-behavior` can additionally stop scrolling from chaining into the underlying page when the sheet reaches its own boundary. Apply it narrowly: containing overscroll can also affect platform navigation/pull-to-refresh gestures.

## Source idea

- https://github.com/viliket/pure-web-bottom-sheet
- https://www.reddit.com/r/css/comments/1on7rhn/

Treat the repository as an architectural experiment; validate accessibility, focus behavior, scroll reachability, and actual mobile ergonomics for your product.
