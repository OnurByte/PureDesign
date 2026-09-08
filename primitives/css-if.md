# CSS `if()` Function

**Status:** experimental / watchlist.

`if()` allows conditional logic inside a CSS property value:

```css
.card {
  padding: if(
    media(width < 40rem): .75rem;
    else: 1.25rem;
  );
}
```

Tests can be based on media, style, or feature conditions.

## Why it matters

It can collapse some conditional custom-property/value plumbing that would otherwise be expressed through duplicated rules or JavaScript-generated inline values.

## PureDesign rule

Do not build required behavior on it yet. MDN marks the feature Limited Availability and experimental.

Always write a valid baseline declaration first:

```css
.card {
  padding: 1rem;
}

@supports (padding: if(media(width > 1px): 1rem; else: 2rem;)) {
  /* optional enhancement */
}
```

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/if
- https://developer.chrome.com/blog/if-article
