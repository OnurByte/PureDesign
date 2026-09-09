# URL-addressable slideshow

## Goal

Build a presentation/deck whose slides can be navigated, deep-linked, refreshed and shared without client-side JavaScript.

## Compose

- [anchor navigation](../primitives/anchor-navigation.md)
- [`:target`](../primitives/target.md)
- [scroll snap](../primitives/scroll-snap.md)
- [scroll offsets](../primitives/scroll-offsets.md)
- optional [CSS scroll buttons and markers](../primitives/scroll-buttons-and-markers.md)

## Baseline

Each slide has a durable fragment identifier and ordinary previous/next links.

```html
<main class="deck" aria-label="Presentation">
  <section class="slide" id="slide-1">
    <h1>Introduction</h1>
    <a href="#slide-2">Next</a>
  </section>

  <section class="slide" id="slide-2">
    <h2>Architecture</h2>
    <a href="#slide-1">Previous</a>
    <a href="#slide-3">Next</a>
  </section>

  <section class="slide" id="slide-3">
    <h2>Conclusion</h2>
    <a href="#slide-2">Previous</a>
  </section>
</main>
```

```css
.deck {
  display: flex;
  overflow-x: auto;
  scroll-snap-type: x mandatory;
}

.slide {
  flex: 0 0 100%;
  min-block-size: 100dvb;
  scroll-snap-align: start;
  scroll-margin-inline: 0;
}

.slide:target {
  outline: .2rem solid currentColor;
  outline-offset: -.2rem;
}
```

The fragment is real navigation state. Browser history, reload, copy-link and opening a slide directly continue to work.

## Optional generated controls

Supporting browsers may add `::scroll-button()` / `::scroll-marker` controls as progressive enhancement. They must not replace the explicit link path until compatibility is sufficient for the target audience.

## Rules

- Keep slide IDs stable when they are shared externally.
- Do not hide every non-`:target` slide; an empty fragment must still leave a usable deck.
- Do not make CSS-generated marker content the only accessible slide title.
- Use normal document content/order so printing, reading mode and unsupported browsers still expose the presentation.

## Ownership

```text
addressed slide -> URL fragment
manual scrolling -> browser scroll state
snap behavior    -> CSS/browser
previous/next    -> real links
slide content    -> document/server
```

## Research provenance

- https://github.com/elitmus/scriptless-slides — early HTML/CSS-only slideshow experiment; the modern PureDesign composition uses real fragment navigation and scroll snap rather than inheriting its historical widget implementation.
