# `::details-content`

**Role:** select the expandable content box of a native `<details>` element separately from its `<summary>`.

The disclosure state still belongs to native HTML; this pseudo-element only gives CSS a direct hook for the content region.

```css
details::details-content {
  opacity: 0;
  transition:
    opacity 180ms,
    content-visibility 180ms allow-discrete;
}

details[open]::details-content {
  opacity: 1;
}
```

Pairing this with intrinsic-size animation can produce richer disclosure motion, but the unanimated `<details>` must remain the complete baseline.

See [`details.md`](details.md) for disclosure semantics and [`interpolate-size.md`](interpolate-size.md) for intrinsic-size animation.

## Compatibility

`::details-content` shipped in Firefox 143. It is newer than the repository's Firefox 140 ESR/Tor baseline, therefore it is polish only for that target.

## Sources

- MDN: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/::details-content
- Web Features: https://web-platform-dx.github.io/web-features-explorer/features/details-content/
- Firefox 143: https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/143
