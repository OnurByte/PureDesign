# Accessible responsive reordering

## Goal

Handle a responsive Grid/Flex layout whose visual order changes without breaking keyboard/screen-reader order or using JavaScript DOM reordering.

## Baseline rule

Write the DOM in the most sensible semantic/readable order first.

Do not start with CSS reordering and try to repair semantics later.

## Progressive direction

Where browser support is explicitly available, `reading-flow` can align sequential navigation with a visual Grid/Flex flow:

```css
.dashboard {
    display: grid;
    grid-template-columns: 18rem 1fr;
}

@supports (reading-flow: grid-rows) {
    .dashboard {
        reading-flow: grid-rows;
    }
}
```

For explicit child groups, study `reading-order`.

## Avoid

- positive `tabindex` values as layout repair
- duplicate desktop/mobile DOM copies containing the same controls
- JavaScript that physically moves interactive elements between containers on resize
- visual reordering that contradicts document meaning

## Status

`reading-flow` is experimental/Limited Availability in 2026. It is an enhancement, not an excuse to ship bad source order.

## Read

- [`../primitives/reading-flow.md`](../primitives/reading-flow.md)
- [`../principles/accessibility-and-input.md`](../principles/accessibility-and-input.md)
- [`../principles/semantic-html-first.md`](../principles/semantic-html-first.md)
