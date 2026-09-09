# `scroll-behavior`

**Role:** let normal fragment/navigation scrolling animate without `scrollTo()` helper JavaScript.

```css
html {
  scroll-behavior: smooth;
}

@media (prefers-reduced-motion: reduce) {
  html {
    scroll-behavior: auto;
  }
}
```

With ordinary links:

```html
<a href="#security">Security</a>
```

browser navigation, URL state and scrolling remain native.

## What it replaces

A narrow script class such as:

```text
intercept anchor click
 -> find target
 -> window.scrollTo({ behavior: smooth })
```

when all you wanted was smooth fragment navigation.

## Rules

- Preserve real fragment links; do not replace them with buttons plus JS.
- Pair with [`scroll-offsets.md`](scroll-offsets.md) for sticky-header clearance.
- Respect [`prefers-reduced-motion.md`](prefers-reduced-motion.md).
- Smooth motion is polish. Core navigation must work with `auto`.

## Source

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/scroll-behavior
