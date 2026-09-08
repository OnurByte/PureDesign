# Progressive Enhancement

## Rule

Functionality must exist before optional modern CSS is applied.

Correct:

```text
baseline HTML/CSS -> usable
new feature       -> better positioning/motion/controls
unsupported       -> still usable
```

Incorrect:

```text
new feature supported   -> component works
new feature unsupported -> task disappears
```

## Recommended structure

```css
.component {
    /* baseline layout and behavior */
}

@media (prefers-reduced-motion: no-preference) {
    .component {
        transition: opacity 120ms ease;
    }
}

@supports (position-anchor: --trigger) {
    .component {
        /* optional enhancement */
    }
}
```

## Enhancement-only examples

Depending on the browser baseline:

- CSS Anchor Positioning
- `@starting-style`
- discrete transitions
- intrinsic-size animation helpers
- CSS-generated carousel controls
- `scroll-target-group`
- `focusgroup`
- `interestfor`
- customizable select styling
- Declarative Partial Updates

Always verify the exact target browser in `compatibility/`.

## Research references

Useful examples of this architecture:

- Adam Bien / unscripted — https://github.com/AdamBien/unscripted
- MinimaCSS — https://github.com/hardikforall/MinimaCSS
- Omni Carousel — https://github.com/demetris/omni-carousel
- TeamDijon details fallback example — https://gist.github.com/TeamDijon
