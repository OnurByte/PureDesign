# `:local-link` Watchlist

**Status:** experimental / unsupported in current browsers as of the 2026-09 research snapshot.

The selector is intended to match links whose target is the current document:

```css
a:local-link {
  font-weight: 700;
}
```

This is interesting for PureDesign because it points toward browser-owned URL-derived link state instead of route-matching JavaScript.

## Do not use for current navigation today

MDN currently reports **no browser support**.

For production current-page/current-step state, use server-rendered [`aria-current`](aria-current.md):

```html
<a href="/settings" aria-current="page">Settings</a>
```

This is also semantically stronger because assistive technology receives the same state that sighted users see.

## Watch direction

Future selector work may make more URL-relative presentation derivable in CSS, but it should remain presentation only. The application/server still owns route meaning.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/:local-link
- Mozilla implementation tracking: https://bugzilla.mozilla.org/show_bug.cgi?id=1943247
