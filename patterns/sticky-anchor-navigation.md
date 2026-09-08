# Sticky Header + Fragment Navigation

## Compose

- [`:target`](../primitives/target.md)
- [`scroll-margin` / `scroll-padding`](../primitives/scroll-offsets.md)

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
}

section[id] {
  scroll-margin-block-start: 1rem;
}
```

## Why

Keep navigation as real URLs/fragments and let the scroll container describe its optimal viewing region. Do not intercept fragment clicks just to subtract the header height in JavaScript.
