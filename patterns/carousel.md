# Carousel

## Compose

- baseline [CSS Scroll Snap](../primitives/scroll-snap.md)
- optional [CSS-generated scroll buttons/markers](../primitives/scroll-buttons-and-markers.md)

## Baseline

```html
<div class="carousel" aria-label="Featured items">
  <article>One</article>
  <article>Two</article>
  <article>Three</article>
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

The baseline is already usable by touchpad, touch, mouse/scrollbar and keyboard/browser scrolling. Newer CSS-generated controls may add buttons and markers without becoming required.

## Rule

Do not make a drag library the existence condition for the carousel content.
