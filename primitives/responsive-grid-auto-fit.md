# Responsive Grid with `repeat(auto-fit, minmax())`

**Role:** let the layout engine choose column count from available space.

```css
.file-grid {
  display: grid;
  gap: 1rem;
  grid-template-columns:
    repeat(auto-fit, minmax(min(14rem, 100%), 1fr));
}
```

This replaces a common frontend pattern:

```text
read container/window width
 -> calculate number of columns
 -> set class such as cols-2 / cols-3 / cols-4
```

with intrinsic Grid layout.

## Why `min(14rem, 100%)`

The nested `min()` keeps the minimum track from overflowing when the container itself is narrower than the preferred card minimum.

## `auto-fit` vs `auto-fill`

- `auto-fit` collapses unused tracks and lets existing items expand.
- `auto-fill` keeps empty tracks reserved.

Choose based on the desired sparse-result behavior. Do not assume one is universally better.

## Boundary

Use this when the same markup should merely reflow.

If the amount/type of data or application behavior changes at a breakpoint, that is not a Grid-column-count problem.

## Sources

- https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Grids
- https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Media_queries
- https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Grid_layout/Common_grid_layouts
- Real project write-up using the RAM pattern: https://github.com/vanzasetia/designo-multi-page-website
- Community discussion: https://www.reddit.com/r/css/comments/183d336/
