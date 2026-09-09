# `sibling-index()` and `sibling-count()`

**Role:** expose an element's DOM sibling position/count as numeric CSS values for calculations.

```css
.item {
  --i: sibling-index();
  --n: sibling-count();
  transition-delay: calc((var(--i) - 1) * 35ms);
}
```

Unlike CSS counters, these functions return numbers that can participate directly in calculations.

## Useful cases

- progressive stagger timing without server-generated index variables;
- geometry derived from item position;
- equal sizing based on direct sibling count;
- decorative progress/ring placement where DOM order is already semantic.

Do not use them to repair an incorrect source order. DOM order remains the semantic/accessibility order.

## Baseline fallback

Prefer mature layout primitives for core behavior:

```css
.list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(14rem, 1fr));
}
```

If an exact item index is required for server-visible behavior, the server can render a class/data/custom property. Do not make `sibling-index()` the only path to a task on the conservative target.

## Compatibility

Firefox 154 added both functions on **2026-08-18**. They are therefore newer than the repository's Firefox 140 ESR/Tor reference target even though current Baseline metadata may describe them as newly available.

## Sources

- MDN `sibling-index()`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/sibling-index
- MDN `sibling-count()`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/sibling-count
- Firefox 154 developer notes: https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/154
- Community discussion: https://www.reddit.com/r/css/comments/1vxqjv7/
