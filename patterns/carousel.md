# Carousel

## Compose

- baseline [CSS Scroll Snap](../primitives/scroll-snap.md)
- optional [CSS-generated scroll buttons/markers](../primitives/scroll-buttons-and-markers.md)

## Baseline

```html
<div class="carousel" aria-label="Featured items">
  <article id="item-1">One</article>
  <article id="item-2">Two</article>
  <article id="item-3">Three</article>
</div>
```

```css
.carousel {
  display: flex;
  gap: 1rem;
  overflow-x: auto;
  scroll-snap-type: x mandatory;
}

.carousel > * {
  flex: 0 0 min(85%, 24rem);
  scroll-snap-align: start;
}
```

The baseline is already usable by touchpad, touch, mouse/scrollbar and keyboard/browser scrolling.

## Progressive generated controls

Newer CSS can ask the browser to generate previous/next buttons and markers from the scroll container itself:

```css
@supports selector(.carousel::scroll-button(left)) {
  .carousel {
    scroll-marker-group: after;
  }

  .carousel::scroll-button(left) {
    content: "←" / "Previous";
  }

  .carousel::scroll-button(right) {
    content: "→" / "Next";
  }

  .carousel > article::scroll-marker {
    content: "";
  }

  .carousel > article::scroll-marker:target-current {
    background: currentColor;
  }
}
```

The browser owns button disabled state at the ends of the scroller and marker state in supporting implementations. Do not recreate those states with client-side JavaScript merely for browsers that already expose the native mechanism.

## Accessibility and fallback

- Keep carousel content in normal document order.
- Do not hide content when generated controls are unsupported.
- Give the scroller a useful accessible label when context does not already provide one.
- Do not put essential item names only in generated `content`.
- Generated controls do not imply infinite looping.

## Rule

Do not make a drag library, generated scroll button, or marker API the existence condition for the carousel content. Scroll snap is the baseline; generated controls are progressive enhancement.
