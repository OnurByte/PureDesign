# `contrast-color()`

**Role:** let CSS choose black or white for maximum contrast against a supplied color.

```css
.badge {
  background: var(--badge-bg);
  color: contrast-color(var(--badge-bg));
}
```

This is useful when a background token is server-selected and maintaining a parallel foreground token would otherwise require duplicated logic.

## Accessibility boundary

`contrast-color()` currently chooses between black and white. Mid-tone colors can still produce a result that is not comfortable/readable enough for small text.

Therefore:

- constrain generated backgrounds to an approved palette;
- keep a tested fallback foreground;
- still test actual contrast instead of treating the function as an accessibility proof.

```css
.badge {
  color: var(--badge-fg, CanvasText);
}

@supports (color: contrast-color(red)) {
  .badge {
    color: contrast-color(var(--badge-bg));
  }
}
```

## Compatibility

`contrast-color()` is Baseline 2026 for current evergreen browsers, but Firefox support starts at Firefox 146. It is newer than the Firefox 140 ESR/Tor baseline, so use it as progressive styling only there.

## Sources

- MDN: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/color_value/contrast-color
- WebKit article: https://webkit.org/blog/16929/contrast-color/
- CSS Color 5: https://drafts.csswg.org/css-color-5/#contrast-color
