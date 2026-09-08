# Micro-Interactions / App Feel

## Compose

- [`:hover` / `:active`](../primitives/interaction-pseudo-classes.md)
- [`:focus-visible` / `:focus-within`](../primitives/focus-states.md)
- [`prefers-reduced-motion`](../primitives/prefers-reduced-motion.md)
- optional [`@starting-style` / discrete transitions](../primitives/starting-style-and-discrete-transitions.md)

## Goal

Make controls respond immediately without introducing a client runtime merely for visual feedback.

```css
.button {
  transition: transform 80ms ease, background 120ms ease;
}

.button:hover { background: var(--hover); }
.button:active { transform: scale(.98); }
.button:focus-visible {
  outline: 2px solid var(--focus);
  outline-offset: 2px;
}

@media (prefers-reduced-motion: reduce) {
  .button {
    transition: none;
  }

  .button:active {
    transform: none;
  }
}
```

## Rules

- keep durations short;
- never hide functionality behind hover;
- preserve strong keyboard focus;
- respect reduced-motion preferences;
- motion must not be required to reach the final state.
