# `text-wrap`

**Role:** let the browser choose better line breaks without measuring text or inserting manual `<br>` elements.

```css
.hero-title {
  text-wrap: balance;
}

.article-copy {
  text-wrap: pretty;
}
```

## Values worth knowing

- `balance` — balances short headings/captions across a limited number of lines.
- `pretty` — uses a more expensive wrapping strategy intended for typographic quality in longer text.
- `stable` — keeps earlier lines more stable while editable text changes.

This can replace narrow JavaScript utilities that:

```text
measure rendered text
 -> try line breaks
 -> inject <br>
 -> re-run on resize/font load
```

## Boundaries

Do not use `balance` as a global default for all body copy. Browsers intentionally limit the number of lines it considers, and community feedback shows it is a design choice rather than a universal improvement.

Keep real content in the DOM. `text-wrap` is presentation only.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/text-wrap
- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/text-wrap-style
- Low-visibility 2026 discussion: https://www.reddit.com/r/css/comments/1qlfynq/
- Earlier community support discussion: https://www.reddit.com/r/Frontend/comments/12hbsw2/
