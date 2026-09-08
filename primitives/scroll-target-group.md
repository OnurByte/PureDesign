# `scroll-target-group` + `:target-current`

**Role:** emerging browser-owned current-section state for scrollspy/navigation highlighting.

```html
<nav class="toc">
  <a href="#intro">Intro</a>
  <a href="#security">Security</a>
  <a href="#storage">Storage</a>
</nav>
```

```css
.toc {
  scroll-target-group: auto;
}

.toc a:target-current {
  font-weight: 700;
  text-decoration: underline;
}
```

## Replaces

```text
IntersectionObserver
 -> calculate active section
 -> remove .active
 -> add .active
```

with browser-owned current-target state.

A useful experimental pattern combines this with Anchor Positioning and `:has()` so one moving indicator can attach to whichever TOC link is current.

## Status

Enhancement-only for conservative Firefox/Tor targets.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/scroll-target-group
- https://github.com/mozilla/standards-positions/issues/1251
- https://gist.github.com/TingRubato/5a8474ed70eae1075f4db90211d510d2
