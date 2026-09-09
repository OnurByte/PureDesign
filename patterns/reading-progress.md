# Reading progress

## Goal

Show a visual reading-position indicator tied to document scrolling without a scroll listener or client-side JavaScript.

## Compose

- [scroll-driven animations](../primitives/scroll-driven-animations.md)
- [`prefers-reduced-motion`](../primitives/prefers-reduced-motion.md)

## Baseline

Reading the document must not depend on the progress indicator. Render it as optional presentation:

```html
<div class="reading-progress" aria-hidden="true">
  <span></span>
</div>

<main>
  ...article content...
</main>
```

```css
.reading-progress {
  position: sticky;
  inset-block-start: 0;
  block-size: .2rem;
  overflow: hidden;
}

.reading-progress > span {
  display: block;
  inline-size: 100%;
  block-size: 100%;
  transform: scaleX(0);
  transform-origin: left;
}
```

Without scroll-driven animation support the bar can remain at its initial presentation or be hidden. Content, navigation and completion remain unchanged.

## Progressive enhancement

```css
@supports (animation-timeline: scroll()) {
  .reading-progress > span {
    animation: reading-progress linear both;
    animation-timeline: scroll(root block);
  }
}

@keyframes reading-progress {
  to {
    transform: scaleX(1);
  }
}
```

The browser's scroll timeline replaces the common pattern of reading `scrollY`, calculating a percentage and mutating a bar on every scroll event.

## Semantics

Do not use a fake `<progress>` value unless you can expose an actual meaningful value. A CSS-only scroll animation changes presentation but does not keep an HTML `value` attribute or accessible numeric state synchronized.

If the product needs a semantic progress value such as "3 of 5 steps completed", render a real `<progress>` from server-known state instead. Scroll position is not the same thing as task completion.

## Reduced motion

The indicator is a direct scroll-linked visual rather than a timed entrance animation, but it is still nonessential. If the chosen treatment adds motion beyond a simple scale, remove that extra motion under `prefers-reduced-motion`.

## Tor / ESR

For the conservative Firefox 140 ESR / Tor Browser 15 target, scroll-driven animation is enhancement-only. Never hide content or controls behind it.

## Research provenance

- https://github.com/ipoly/scroll-state-lab — demonstrates a zero-JS scroll-timeline progress bar tied to a scroll container.
- https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_scroll-driven_animations
