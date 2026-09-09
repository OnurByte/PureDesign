# CSS Custom Functions with `@function`

**Role:** define reusable value-producing CSS logic without a client runtime.

```css
@function --space(--step <number>) returns <length> {
  result: calc(var(--space-unit) * var(--step));
}

.card {
  padding: --space(4);
}
```

Custom functions can accept arguments and return CSS values. Newer syntax can combine them with conditional CSS logic.

## What this is for

- design-system calculations;
- reusable color/spacing transformations;
- reducing duplicated complex value expressions.

## What this is not for

Do not turn CSS into application business logic. URL/server state, permissions, data fetching and durable mutations still belong outside CSS.

For widely compatible reusable values, custom properties and ordinary functions such as `calc()`, `min()`, `max()`, `clamp()` and `color-mix()` remain the baseline.

## Compatibility

`@function` shipped in Chromium 139. As of the 2026-09-09 snapshot, Firefox has no normal release support, so it is a watchlist primitive and cannot participate in Tor/Firefox 140 core behavior.

## Sources

- MDN guide: https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Custom_functions_and_mixins/Using_custom_functions
- MDN `@function`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/@function
- CSS Functions and Mixins: https://drafts.csswg.org/css-mixins-1/
