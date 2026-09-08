# `:open`

**Role:** Stable browser-state selector in the Firefox 140 ESR baseline.

`:open` provides a common selector for elements that expose an open/closed state.

```css
details:open > summary {
    font-weight: 700;
}

dialog:open {
    opacity: 1;
}

select:open {
    outline-color: var(--accent);
}
```

Depending on the element/browser capability, it can apply to things such as:

- `<details>`
- `<dialog>`
- picker-capable `<select>` / `<input>` elements

## Replaces

Element-specific state classes that JavaScript would otherwise toggle only for styling:

```text
.open
.is-expanded
.dialog-visible
```

Prefer the browser's actual state.

## Fallbacks

Where `:open` support is not guaranteed, mature elements often expose an attribute/state-specific selector:

```css
details[open] { ... }
dialog[open] { ... }
```

Popover uses its own `:popover-open` state.

## Firefox/Tor relevance

Firefox added `:open` in Firefox 136, before the Firefox 140 ESR baseline used by Tor Browser 15.0.21.

## Sources

- MDN pseudo-class reference: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/Pseudo-classes
- MDN `<details>`: https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/details
- MDN `<dialog>`: https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/dialog
- Firefox 136 release notes: https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/136
