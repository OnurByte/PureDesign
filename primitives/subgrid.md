# CSS Subgrid

**Role:** let nested Grid items inherit parent track sizing instead of measuring siblings in JavaScript.

```css
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(16rem, 1fr));
}

.card {
  display: grid;
  grid-row: span 3;
  grid-template-rows: subgrid;
}
```

This is especially useful when repeated cards should align internal rows such as:

```text
title
metadata
footer/action
```

across neighboring cards despite different content lengths.

## What it replaces

A class of layout scripts that:

```text
measure all card headings
 -> find max height
 -> set inline heights
 -> repeat on resize/content/font changes
```

Subgrid allows descendants to participate in tracks established by the parent grid.

## Boundary

Subgrid solves **alignment**, not arbitrary equal-height product logic. Keep semantic content in natural order and let layout tracks do the alignment.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Grid_layout/Subgrid
- MDN card cookbook notes subgrid as the hack-free way to align card internals: https://developer.mozilla.org/en-US/docs/Web/CSS/How_to/Layout_cookbook/Card
