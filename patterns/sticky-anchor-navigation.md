# Sticky Header + Fragment Navigation

## Compose

- [real anchor navigation](../primitives/anchor-navigation.md)
- [`:target`](../primitives/target.md)
- [`scroll-margin` / `scroll-padding`](../primitives/scroll-offsets.md)
- optional [`scroll-behavior`](../primitives/scroll-behavior.md)
- [`prefers-reduced-motion`](../primitives/prefers-reduced-motion.md)

```html
<nav>
  <a href="#account">Account</a>
  <a href="#security">Security</a>
</nav>

<section id="account">...</section>
<section id="security">...</section>
```

```css
html {
  scroll-padding-block-start: 4.5rem;
  scroll-behavior: smooth;
}

section[id] {
  scroll-margin-block-start: 1rem;
}

@media (prefers-reduced-motion: reduce) {
  html {
    scroll-behavior: auto;
  }
}
```

## Why

Keep navigation as real URLs/fragments and let the scroll container describe its optimal viewing region.

Do not intercept fragment clicks just to:

```text
measure sticky header
 -> subtract height
 -> window.scrollTo()
```

Smooth scrolling is optional polish; fragment navigation itself must remain functional without it.
