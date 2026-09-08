# Responsive Component Without ResizeObserver

## Compose

- [Container Size Queries](../primitives/container-size-queries.md)
- ordinary Grid/Flex layout

```html
<section class="widget-shell">
  <article class="widget">
    <h2>Storage</h2>
    <p>1.4 TB used</p>
  </article>
</section>
```

```css
.widget-shell {
  container-type: inline-size;
}

.widget {
  display: grid;
  grid-template-columns: auto 1fr;
}

@container (width < 28rem) {
  .widget {
    grid-template-columns: 1fr;
  }
}
```

## Rule

Use this only when the semantic HTML can remain identical at every size. If width changes the data or actual application structure, CSS is not the owner of that state.

This is the preferred PureDesign replacement for width-only `ResizeObserver -> class toggle` code.
