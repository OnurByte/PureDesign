# `:lang()`

**Role:** derive language-specific presentation from semantic document language instead of injecting locale classes in JavaScript.

```html
<blockquote lang="tr">...</blockquote>
<blockquote lang="en">...</blockquote>
```

```css
blockquote:lang(tr) {
  quotes: "“" "”";
}

code:lang(ja) {
  font-family: var(--jp-mono-stack);
}
```

`:lang()` matches an element according to its language, including inherited language metadata, not merely whether the element itself contains a matching `lang` attribute.

## Boundary

Content/document language -> HTML/server/browser.

Language-specific typography/presentation -> CSS.

Do not use `:lang()` to hide/choose translated application content. Localization content selection belongs to routing/server/application logic.

## Compose

- server-render the real `lang` on the document/content.
- use [`dir()`](dir-pseudo-class.md) only when direction also requires a presentation adjustment.

## Source

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/:lang
