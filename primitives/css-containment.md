# CSS Containment

**Role:** tell the browser that a subtree is sufficiently independent so layout/paint/style work can be scoped.

```css
.file-card {
  contain: layout paint;
}
```

Useful containment modes include:

- `layout`
- `paint`
- `size`
- `inline-size`
- `content`
- combinations of the above

## What this replaces

Not application logic. It replaces a class of manual performance work where code tries to reduce the blast radius of layout/repaint by restructuring runtime behavior.

Containment lets the rendering engine make stronger assumptions itself.

## Footguns

Containment changes behavior, not just performance:

- layout/paint containment creates new containing/formatting contexts;
- some modes create a stacking context;
- `size` containment can make an element act as though its children do not contribute to size;
- fixed/absolute descendants may resolve differently.

Do not apply `contain: strict` globally as a magic optimization.

For off-screen render skipping, see [`content-visibility.md`](content-visibility.md).
For placeholder sizing under size containment, see [`contain-intrinsic-size.md`](contain-intrinsic-size.md).

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/contain
- https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Containment/Using
