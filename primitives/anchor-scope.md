# `anchor-scope`

**Role:** Progressive enhancement / composition primitive for CSS Anchor Positioning.

Repeated server-rendered components may reuse the same anchor name. Without scoping, a positioned descendant can accidentally resolve an anchor from another component instance.

`anchor-scope` limits anchor-name resolution to the intended subtree.

```css
.action-cell {
    anchor-scope: --action-trigger;
}

.action-cell > button {
    anchor-name: --action-trigger;
}

.action-cell > [popover] {
    position-anchor: --action-trigger;
}
```

## Why this matters for PureDesign

Server rendering often repeats components in loops:

```text
file row
file row
file row
...
```

Each row should be self-contained. `anchor-scope` moves overlay association toward CSS component locality instead of generating unique runtime IDs/names just to prevent cross-instance positioning mistakes.

You still need unique HTML `id` values for declarative invoker relationships such as `popovertarget`; `anchor-scope` only scopes CSS anchor names.

## Compatibility

MDN marks `anchor-scope` as Baseline 2026 across current browsers. It depends on the newer Anchor Positioning stack and is not a Tor Browser 15 / Firefox 140 ESR core primitive.

## Sources

- MDN: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/anchor-scope
- CSS Anchor Positioning overview: https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Anchor_positioning
