# CSS Counters

**Role:** browser-maintained presentational numbering derived from document structure.

```css
.steps {
  counter-reset: step;
}

.steps > li::before {
  counter-increment: step;
  content: counter(step) ". ";
}
```

Counters can also represent nested numbering through `counters()`.

## What this replaces

Purely presentational scripts that walk DOM nodes to add visible sequence numbers.

## Boundary

If the number has application meaning — invoice line number, database rank, pagination index, audit sequence — render the authoritative value from the server.

CSS counters are appropriate when numbering follows document structure and is presentation only.

Prefer semantic `<ol>` when ordinary ordered-list numbering already fits. Do not introduce custom counters when native list markers solve the problem.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Counter_styles/Using_counters
- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/counter
- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/counters
