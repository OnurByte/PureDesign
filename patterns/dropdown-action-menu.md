# Dropdown / Action Menu

## Compose

- [Popover API](../primitives/popover.md)
- optional [CSS Anchor Positioning](../primitives/anchor-positioning.md)
- optional [entry/exit transitions](../primitives/starting-style-and-discrete-transitions.md)

## Baseline

```html
<button popovertarget="file-actions">Actions</button>

<div id="file-actions" popover>
  <a href="/files/1/rename">Rename</a>
  <form action="/files/1/delete" method="post">
    <button type="submit">Delete</button>
  </form>
</div>
```

## Positioning

Use ordinary CSS positioning as the baseline. Add Anchor Positioning only inside a compatibility-safe enhancement path.

## State ownership

Open/close -> browser. Mutating an item -> form/server. Visual motion -> CSS.
