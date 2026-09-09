# Stable Scroll Content

Use this for long reading/list surfaces where late layout changes should not throw the user's viewport around.

## First reserve space

```html
<img
  src="/preview/42.webp"
  alt="Preview"
  width="800"
  height="450">
```

Intrinsic dimensions or `aspect-ratio` prevent many shifts before scroll anchoring needs to help.

## Let the browser anchor by default

Do not disable scroll anchoring globally. Only exclude a known bad candidate:

```css
.live-banner {
  overflow-anchor: none;
}
```

The rest of the scroll container keeps normal browser anchoring behavior where supported.

## What not to claim

```text
scroll anchoring != virtualization
scroll anchoring != pagination
scroll anchoring != permission to omit media dimensions
```

Use server pagination/data limits and rendering containment separately when needed.

## Read

- [`../primitives/overflow-anchor.md`](../primitives/overflow-anchor.md)
- [`../primitives/aspect-ratio-and-object-fit.md`](../primitives/aspect-ratio-and-object-fit.md)
- [`../primitives/content-visibility.md`](../primitives/content-visibility.md)
- [`server-filter-sort-pagination.md`](server-filter-sort-pagination.md)
