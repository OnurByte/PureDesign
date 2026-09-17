# Tabular Numerals with `font-variant-numeric`

**Role:** keep changing or indexed numbers visually aligned without measuring text in JavaScript.

```html
<ol class="recovery-words">
  <li><span class="index">1.</span> maple</li>
  <li><span class="index">10.</span> velvet</li>
</ol>
```

```css
.index {
  inline-size: 2.5ch;
  font-variant-numeric: tabular-nums;
  color: var(--muted);
}
```

`tabular-nums` asks the font for equal-width numeral glyphs so values such as `1`, `8`, `10` and `12` line up more cleanly in counters, tables, timers and ordered credential lists.

## Font boundary

This relies on the active font exposing suitable OpenType numeric features. If the font does not provide tabular figures, the declaration may have little or no visible effect. Reserve enough inline space so alignment does not depend on the feature alone.

## Use when

- recovery phrase indexes;
- financial/statistical tables;
- timers and counters;
- compact numeric metadata that benefits from stable glyph width.

Do not use it as a substitute for actual table/grid alignment when columns have semantic structure.

## Source

- https://developer.mozilla.org/en-US/docs/Web/CSS/font-variant-numeric
