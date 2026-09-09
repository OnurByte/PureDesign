# CSS `interactivity`

**Role:** newer CSS mechanism for making an element subtree inert.

```css
.preview[aria-hidden="true"] {
  interactivity: inert;
}
```

The inert state prevents interaction/focus and affects discoverability in ways similar to the HTML `inert` attribute.

## Prefer HTML for known state

If the server already knows a subtree is inactive, use the mature semantic attribute:

```html
<section inert>...</section>
```

See [`inert.md`](inert.md).

The CSS property becomes interesting when inertness can be derived from CSS-owned presentation state, for example future scroll-driven paginated interfaces.

## Security boundary

`interactivity: inert` is a UI interaction mechanism, **not authorization**. Hidden/inert controls do not replace server permission checks.

## Accessibility boundary

Making content inert can remove links/controls from keyboard and accessibility navigation. The inactive state must be understandable without relying only on visual dimming.

## Compatibility

As of the 2026-09-09 research snapshot, Chromium supports this property from Chrome 135; Firefox and Safari do not provide normal release support. It is not usable for Firefox 140/Tor core behavior.

## Sources

- MDN: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/interactivity
- HTML `inert`: https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes/inert
- CSS Basic UI Level 4: https://drafts.csswg.org/css-ui-4/#inertness
