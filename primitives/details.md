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

## State

The durable source of UI state is the element itself:

```css
details[open] > summary {
    font-weight: 700;
}
```

Firefox 136+ also supports the generic `:open` selector:

```css
details:open > summary {
    font-weight: 700;
}
```

## Animation boundary

Do not confuse mature disclosure behavior with newer animation hooks.

- `<details>` itself is mature.
- grouped `<details name>` landed in Firefox 130.
- `:open` landed in Firefox 136.
- `::details-content` landed in Firefox 143, **newer than Firefox 140 ESR**.
- intrinsic-size interpolation is additional polish and must not be required.

For Tor Browser 15 / Firefox 140 ESR, use the native disclosure behavior and ordinary `[open]`/`:open` styling; do not require `::details-content`.

## Rules

- Prefer this over a hidden-checkbox disclosure.
- Keep the unanimated element fully usable.
- Long auto-closing accordion panels can cause unpleasant mobile scroll jumps; test real content.

## Sources

- MDN: https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/details
- Firefox 130: https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/130
- Firefox 136 (`:open`): https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/136
- Firefox 143 (`::details-content`): https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/143
- Small progressive animation gist: https://gist.github.com/TeamDijon
- Community edge cases: https://www.reddit.com/r/css/comments/1vwv16h/
