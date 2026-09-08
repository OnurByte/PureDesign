# CSS `@scope`

**Role:** confine selectors to a component subtree without Shadow DOM or runtime-generated class names.

```css
@scope (.file-card) to (.file-card__preview) {
  button {
    border-radius: .5rem;
  }
}
```

`@scope` can reduce selector specificity/DOM coupling for server-rendered components while keeping the DOM in the light tree.

## Why it fits PureDesign

Before reaching for:

- runtime CSS-in-JS scoping;
- generated class hashes;
- Shadow DOM solely for style isolation;

check whether ordinary cascade layers/selectors or `@scope` already solve the problem.

## Compatibility

MDN marks `@scope` as Baseline 2026. That means current browsers, not old ESR targets. Do not assume Firefox 140/Tor support from the Baseline label.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/%40scope
