# `:modal` / `::backdrop`

**Role:** style browser-owned modal/top-layer state without `.is-modal` class bookkeeping.

```css
dialog:modal {
  border: 0;
  border-radius: 1rem;
}

dialog:modal::backdrop {
  background: rgb(0 0 0 / .5);
}
```

`:modal` matches elements in a state that excludes interaction with the rest of the document until dismissed. For `<dialog>` shown modally, the browser also creates a `::backdrop` pseudo-element and makes the rest of the document inert.

Firefox supports `:modal` since Firefox 103, so it is inside the Firefox 140 ESR engine baseline.

## Why

Avoid state duplication such as:

```text
show modal
 -> add body.modal-open
 -> add dialog.open
 -> create overlay div
 -> synchronize close state
```

when the browser already owns modal/top-layer state.

## Boundary

The selector does not open a dialog. Use the compatible declarative/opening path appropriate for the target browser.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/%3Amodal
- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/::backdrop
- https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/103
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/dialog
