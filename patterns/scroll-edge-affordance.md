# Scroll edge affordance

## Goal

Indicate that a scroll region still has hidden content above or below without a scroll listener, `IntersectionObserver`, or client-side JavaScript.

## Compose

- [scroll-state container queries](../primitives/scroll-state-container-queries.md)
- [`position: sticky`](../primitives/position-sticky.md)
- [`overscroll-behavior`](../primitives/overscroll-behavior.md) only when nested-scroll chaining actually needs control

## Baseline

The content must remain fully usable as a normal scroll region without any edge-state styling.

```html
<div class="scroll-region">
  <div class="edge-cue edge-cue-top" aria-hidden="true"></div>

  <ul>
    <li>...</li>
    <li>...</li>
    <li>...</li>
  </ul>

  <div class="edge-cue edge-cue-bottom" aria-hidden="true"></div>
</div>
```

```css
.scroll-region {
  max-block-size: 24rem;
  overflow: auto;
}

.edge-cue {
  position: sticky;
  z-index: 1;
  block-size: 1rem;
  pointer-events: none;
  opacity: 0;
}

.edge-cue-top {
  inset-block-start: 0;
  background: linear-gradient(to bottom, rgb(0 0 0 / .18), transparent);
}

.edge-cue-bottom {
  inset-block-end: 0;
  background: linear-gradient(to top, rgb(0 0 0 / .18), transparent);
}
```

Without the enhancement the cues stay hidden and scrolling still works.

## Progressive enhancement

```css
@supports (container-type: scroll-state) {
  .scroll-region {
    container-name: scroll-region;
    container-type: scroll-state;
  }

  @container scroll-region scroll-state(scrollable: top) {
    .edge-cue-top {
      opacity: 1;
    }
  }

  @container scroll-region scroll-state(scrollable: bottom) {
    .edge-cue-bottom {
      opacity: 1;
    }
  }
}
```

`scrollable: top` means content exists beyond the top edge; `scrollable: bottom` means more content remains below. The browser derives those states from scrolling.

## Rule

Treat the cue as presentation, not as the only way users learn that content exists. Scrollbars, content structure and ordinary scrolling remain the functional baseline.

Do not substantially resize the query container in response to its own scroll state. Prefer opacity, color, shadow or another paint-only change.

## Tor / ESR

Firefox 140 ESR / Tor Browser 15 cannot use scroll-state queries as core behavior. The normal scroll container is the baseline; the edge cue is progressive enhancement only.

## Research provenance

- https://github.com/ipoly/scroll-state-lab — small pure-CSS experiment combining `scroll-state(scrollable: ...)` with sticky edge surfaces.
- https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Conditional_rules/Container_scroll-state_queries
