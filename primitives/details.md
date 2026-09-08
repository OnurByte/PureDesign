# `<details>` / `<summary>`

**Role:** browser-owned disclosure state.

Use for FAQs, expandable settings, metadata sections and simple accordions.

```html
<details>
  <summary>Security</summary>
  <p>Security settings...</p>
</details>
```

Grouped accordion behavior:

```html
<details name="settings"><summary>Security</summary>...</details>
<details name="settings"><summary>Storage</summary>...</details>
```

CSS observes `[open]`; newer browsers also expose richer animation hooks such as `::details-content`.

## Rules

- Prefer this over a hidden-checkbox disclosure.
- Keep the unanimated element fully usable.
- Long auto-closing accordion panels can cause unpleasant mobile scroll jumps; test real content.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/details
- https://gist.github.com/TeamDijon
- https://www.reddit.com/r/css/comments/1vwv16h/
- https://www.reddit.com/r/css/comments/1g4d2aa/
