# Current Navigation Without Route-Matching JavaScript

## Compose

- [real anchor navigation](../primitives/anchor-navigation.md)
- [`aria-current`](../primitives/aria-current.md)

The server already knows which page it rendered. Put that truth in the HTML:

```html
<nav aria-label="Primary">
  <a href="/files" aria-current="page">Files</a>
  <a href="/shares">Shares</a>
  <a href="/settings">Settings</a>
</nav>
```

```css
nav a[aria-current="page"] {
  font-weight: 700;
  background: var(--current-bg);
}
```

## Avoid

```text
DOMContentLoaded
 -> read location.pathname
 -> loop all navigation links
 -> compare href
 -> add .active
```

That recreates state the URL/router/server already knows.

## Other uses

- `aria-current="step"` for multi-page workflows
- `aria-current="page"` for pagination
- `aria-current="location"` for location indicators

Do not confuse `current` with `selected` widget state.
