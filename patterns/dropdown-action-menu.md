# Dropdown / Action Menu

## Compose

- [Popover API](../primitives/popover.md)
- [explicit Popover show/hide/toggle actions](../primitives/popovertargetaction.md)
- optional [CSS Anchor Positioning](../primitives/anchor-positioning.md)
- optional [anchor scoping](../primitives/anchor-scope.md) for repeated components
- optional [anchor-aware visibility](../primitives/position-visibility.md)
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

Open/close belongs to the browser. The actual action remains a link/form/server operation.

## Explicit show/hide controls

When a panel should not merely toggle:

```html
<button popovertarget="filters" popovertargetaction="show">Filters</button>
<div id="filters" popover="manual">
  ...
  <button popovertarget="filters" popovertargetaction="hide">Cancel</button>
</div>
```

This is older/more conservative than generic `command/commandfor` and is available in the Firefox 140 ESR engine baseline through Firefox's Popover support.

## Positioning

Use ordinary CSS positioning as the conservative baseline. Add Anchor Positioning only inside a compatibility-safe enhancement path.

For repeated rows/cards, `anchor-scope` can prevent CSS anchor names from accidentally resolving across component instances. Where an overlay becomes meaningless after its anchor disappears, `position-visibility` can eventually replace scroll/intersection visibility bookkeeping.

## State ownership

```text
open/close       -> browser popover state
position         -> CSS layout
anchor visibility-> CSS layout (newer enhancement)
mutating item    -> form/server
motion           -> CSS polish
```
