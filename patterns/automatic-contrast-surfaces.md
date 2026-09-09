# Automatic Contrast Surfaces

Use this when the server/theme system already provides a background color token and modern browsers can progressively choose black/white foreground text.

```html
<span class="tag" style="--tag-bg: #5b35d5">Research</span>
```

```css
.tag {
  background: var(--tag-bg);
  color: white; /* tested fallback for the approved palette */
}

@supports (color: contrast-color(red)) {
  .tag {
    color: contrast-color(var(--tag-bg));
  }
}
```

## Server-owned user choice

If a user chooses a color via a normal form, persist it on the server and render the resulting token on the next response. Do not add JavaScript merely to mirror an `<input type="color">` value into CSS state.

## Guardrails

- use an approved light/dark palette when possible;
- do not assume `contrast-color()` proves WCAG compliance for every mid-tone;
- keep forced-colors and user contrast preferences working;
- losing the function must not make text disappear.

## Read

- [`../primitives/contrast-color.md`](../primitives/contrast-color.md)
- [`../primitives/forced-colors.md`](../primitives/forced-colors.md)
- [`../primitives/prefers-contrast.md`](../primitives/prefers-contrast.md)
- [`../primitives/color-scheme.md`](../primitives/color-scheme.md)
