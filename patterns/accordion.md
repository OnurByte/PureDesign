# Accordion

## Use

FAQ, settings groups, expandable metadata.

## Compose

- [`<details>` / `<summary>`](../primitives/details.md)
- [`:open`](../primitives/open-pseudo-class.md) where supported; `[open]` remains a straightforward fallback
- optional [`interpolate-size`](../primitives/interpolate-size.md) for intrinsic-size animation
- optional [`@starting-style` / discrete transitions](../primitives/starting-style-and-discrete-transitions.md)

## Baseline

```html
<details name="settings">
  <summary>Security</summary>
  <div class="panel">...</div>
</details>

<details name="settings">
  <summary>Storage</summary>
  <div class="panel">...</div>
</details>
```

Open/closed state belongs to `<details>`, not a hidden checkbox or client class.

## State styling

```css
details[open] > summary,
details:open > summary {
  font-weight: 700;
}
```

## Animation rule

Intrinsic-size interpolation can remove the old JavaScript pattern of measuring `scrollHeight` just to animate to/from `auto`. However, animation remains optional polish.

The accordion must still open instantly and correctly if:

- intrinsic-size animation is unsupported;
- author CSS is reduced;
- `prefers-reduced-motion` requests less motion.

## UX rule

Test long panels on mobile; grouped `details[name]` auto-close behavior can shift scroll position when one long disclosure closes as another opens.
