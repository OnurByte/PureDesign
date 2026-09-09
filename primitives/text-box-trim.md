# `text-box-trim` / `text-box-edge`

**Role:** trim font metric space above/below text for more predictable visual alignment without measurement JavaScript or negative-margin hacks.

Typical use is small UI labels, pills, badges and headings where cap/line-box whitespace makes optical centering difficult.

```css
.label {
  text-box-trim: trim-both;
  text-box-edge: cap alphabetic;
}
```

Treat this as typography polish. The component must remain correctly sized and usable when the declarations are ignored.

## Do not

- use trimming to compensate for broken line-height/layout architecture;
- assume every font/script has the same desirable trim edge;
- make touch target height depend on trimmed glyph bounds.

Interactive target size should come from padding/min-size, not from text metrics alone.

## Compatibility

Firefox 154 added `text-box-trim`, `text-box-edge` and the `text-box` shorthand on **2026-08-18**. That is newer than Firefox 140 ESR/Tor, so this is progressive presentation only for the conservative target.

## Sources

- Firefox 154 release notes: https://www.firefox.com/en-US/firefox/154.0/releasenotes/
- MDN Firefox 154 developer notes: https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/154
- CSS Inline Layout Level 3: https://drafts.csswg.org/css-inline-3/#leading-trim
