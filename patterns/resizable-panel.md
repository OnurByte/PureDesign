# User-Resizable Panel

## Compose

- [`resize`](../primitives/resize.md)
- logical size constraints
- ordinary overflow

```css
.notes-panel {
  resize: vertical;
  overflow: auto;
  min-block-size: 8rem;
  max-block-size: 70dvh;
}
```

For a simple editor/notes/details pane this can avoid a custom drag handle and pointer-event state machine.

## Use when

The requirement is literally:

> Let the user resize this box.

## Do not use as a fake replacement for

- synchronized split panes
- persisted pane percentages
- snap-to-layout behavior
- resize-driven application/data changes

Those are larger interaction/state problems.

Because arbitrary-element `resize` support is not universal, keep the default static panel usable when the resizing affordance is absent.
