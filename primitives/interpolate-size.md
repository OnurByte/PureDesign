# `interpolate-size` and intrinsic-size transitions

**Role:** Polish/progressive enhancement. Never required for disclosure or layout functionality.

Historically, CSS could not smoothly transition between a numeric size and intrinsic keywords such as `auto`, so JavaScript often measured element heights before accordion/drawer animations.

`interpolate-size: allow-keywords` opts into intrinsic-size interpolation.

```css
:root {
    interpolate-size: allow-keywords;
}

.panel {
    block-size: 0;
    overflow: clip;
    transition: block-size 180ms ease;
}

.panel[data-open="true"] {
    block-size: auto;
}
```

For semantic components, derive open state from native state rather than inventing `data-open` client state, for example `<details>` / `::details-content` where supported.

## Replaces

Animation-only scripts such as:

```text
measure scrollHeight
 -> write pixel height
 -> animate
 -> reset to auto
```

## `calc-size()`

`calc-size()` can perform calculations with intrinsic sizes and also enables interpolation for the value it produces. It remains less widely available; use it only when calculations are actually necessary.

## Rule

The closed/open interaction must work with animation disabled and with unsupported interpolation. This primitive is polish, not behavior.

Respect `prefers-reduced-motion`.

## Sources

- MDN `interpolate-size`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/interpolate-size
- MDN `calc-size()`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/calc-size
- Community compatibility caution: https://www.reddit.com/r/css/comments/1r4mg7j/
