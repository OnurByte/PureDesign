# Responsive Card / File Grid

## Compose

- [`repeat(auto-fit, minmax())`](../primitives/responsive-grid-auto-fit.md)
- optional [container size queries](../primitives/container-size-queries.md) when card internals also need to adapt
- optional [`subgrid`](../primitives/subgrid.md) for aligned internals

## Baseline

```css
.items {
  display: grid;
  gap: 1rem;
  grid-template-columns:
    repeat(auto-fit, minmax(min(14rem, 100%), 1fr));
}
```

The browser determines how many columns fit. No `resize` listener and no `cols-1/2/3/4` JavaScript state.

If each reusable card needs a different internal layout based on the **card's own width**, add a container query rather than viewport JS.

## Sparse-result caveat

`auto-fit` lets a small number of items stretch. If that looks wrong for your product, constrain card/item max sizes or choose `auto-fill` deliberately. Do not treat the one-line Grid pattern as universally perfect.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Grid_layout/Common_grid_layouts
- https://github.com/vanzasetia/designo-multi-page-website
- https://www.reddit.com/r/css/comments/183d336/
