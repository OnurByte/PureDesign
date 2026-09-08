# Sticky Header State Without Scroll JavaScript

## Goal

Give a sticky header a visible "stuck" state without an `IntersectionObserver` or scroll listener.

## Baseline

Use [`position: sticky`](../primitives/position-sticky.md):

```css
.header-shell {
    position: sticky;
    inset-block-start: 0;
    z-index: 10;
}
```

The sticky behavior itself is stable browser functionality. The header must remain correct without any state-dependent styling.

## Progressive enhancement

Use [scroll-state container queries](../primitives/scroll-state-container-queries.md) only for extra stuck-state presentation:

```css
@supports (container-type: scroll-state) {
    .header-shell {
        container-type: scroll-state;
    }

    @container scroll-state(stuck: top) {
        .header-ui {
            background: Canvas;
            box-shadow: 0 1px 8px rgb(0 0 0 / .14);
        }
    }
}
```

Use an inner `.header-ui` because container queries style descendants of the query container.

## Avoid the 2026 flicker trap

Do not substantially change sticky-container height/padding in response to `stuck`. That can change the condition being queried and create a feedback loop.

Prefer paint-only feedback:

- shadow
- background
- color
- opacity
- border color

## Ownership

```text
sticky position -> browser layout
stuck state     -> browser scroll state
visual feedback -> CSS
```

## Read

- [`../primitives/position-sticky.md`](../primitives/position-sticky.md)
- [`../primitives/scroll-state-container-queries.md`](../primitives/scroll-state-container-queries.md)
- [`../principles/progressive-enhancement.md`](../principles/progressive-enhancement.md)
