# `aria-current`

**Role:** expose server-known current-location/current-step state semantically without client route-matching JavaScript.

For navigation:

```html
<nav aria-label="Primary">
  <a href="/files" aria-current="page">Files</a>
  <a href="/settings">Settings</a>
</nav>
```

CSS can derive presentation directly:

```css
[aria-current="page"] {
  font-weight: 700;
  text-decoration-thickness: .14em;
}
```

## Useful values

- `page`
- `step`
- `location`
- `date`
- `time`
- `true`

Only one item in a related set should normally be marked current.

## What this replaces

```text
client reads location.pathname
 -> compares every nav URL
 -> toggles .active
```

when the server already knows which route/page/step it rendered.

## Boundary

Current application location/step -> server/URL.

Semantic exposure -> `aria-current`.

Visual treatment -> CSS.

Do not use `aria-current` as a replacement for `aria-selected`; selection and current location are different concepts.

## Source

- https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Reference/Attributes/aria-current
