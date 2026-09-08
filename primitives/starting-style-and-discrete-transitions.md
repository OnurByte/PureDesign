# `@starting-style` and Discrete Transitions

**Role:** animate entry/exit states such as popovers and disclosures without JavaScript timing hooks.

```css
[popover] {
  opacity: 0;
  transform: translateY(-.35rem) scale(.98);
  transition:
    opacity 120ms ease,
    transform 120ms ease,
    display 120ms allow-discrete;
}

[popover]:popover-open {
  opacity: 1;
  transform: none;
}

@starting-style {
  [popover]:popover-open {
    opacity: 0;
    transform: translateY(-.35rem) scale(.98);
  }
}
```

## Rule

Motion is polish. If these features are unsupported, the component must switch state instantly and remain fully usable.

Respect `prefers-reduced-motion`.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/@starting-style
- https://developer.mozilla.org/en-US/docs/Web/CSS/transition-behavior
- https://github.com/hardikforall/MinimaCSS
