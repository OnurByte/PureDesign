# `scroll-margin` / `scroll-padding`

**Role:** anchor and snap landing offsets owned by CSS instead of scroll-position JavaScript.

A sticky header often hides fragment targets:

```css
:root {
  scroll-padding-block-start: 5rem;
}

[id] {
  scroll-margin-block-start: 5rem;
}
```

Now normal links keep working:

```html
<a href="#security">Security</a>
<section id="security">...</section>
```

## Replaces

- `scrollIntoView()` offset calculations
- `window.scrollTo(targetY - headerHeight)`
- arbitrary spacer elements before anchors

## Boundary

Layout shift after navigation can still make the final position appear wrong. Fix unstable layout rather than compensating with more scroll JavaScript.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/scroll-margin
- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/scroll-padding
- https://www.reddit.com/r/css/comments/1kgds99/
- https://www.reddit.com/r/css/comments/1fs9awt/
