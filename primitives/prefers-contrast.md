# `prefers-contrast`

**Role:** adapt presentation to a user-requested contrast preference without JavaScript preference detection.

```css
.control {
  border: 1px solid var(--border);
}

@media (prefers-contrast: more) {
  .control {
    border-width: 2px;
    outline: 1px solid currentColor;
  }
}
```

Firefox enabled `prefers-contrast` by default in Firefox 101, so it is inside the Firefox 140 ESR engine baseline.

## Rule

Use it for targeted readability improvements, not to create a completely separate application theme that drifts from the semantic baseline.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/%40media/prefers-contrast
- https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/101
