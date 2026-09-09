# Balanced Heading Without Line-Break JavaScript

## Compose

- [`text-wrap`](../primitives/text-wrap.md)

```css
.page-title,
.card-title {
  text-wrap: balance;
}
```

This lets the browser choose balanced line breaks for short headings without scripts that measure line lengths or inject `<br>` elements.

For longer prose, consider `text-wrap: pretty` selectively rather than balancing everything.

## Rules

- Heading text remains ordinary semantic text.
- Do not hard-code line breaks solely for one viewport width.
- Do not globally apply typographic wrapping modes without evaluating visual and performance impact.
- This is presentation only; unsupported browsers should simply use normal wrapping.

Community feedback is mixed enough that PureDesign treats this as a deliberate typography choice, not a mandatory reset.

Source discussion: https://www.reddit.com/r/css/comments/1qlfynq/
