# CSS Scroll Buttons and Markers

**Role:** emerging browser-generated controls/state for scroll containers and carousels.

Relevant primitives:

- `::scroll-button()`
- `scroll-marker-group`
- `::scroll-marker-group`
- `::scroll-marker`
- `:target-current`
- `:target-before`
- `:target-after`

Example enhancement:

```css
.carousel {
  display: flex;
  overflow-x: auto;
  scroll-snap-type: x mandatory;
  scroll-marker-group: after;
}

.carousel::scroll-button(left) {
  content: "←" / "Previous";
}

.carousel::scroll-button(right) {
  content: "→" / "Next";
}

.carousel > article::scroll-marker {
  content: "";
}

.carousel > article::scroll-marker:target-current {
  background: currentColor;
}
```

## Rule

The baseline carousel remains a normal usable scroll-snap container. Generated controls are enhancement-only until the browser matrix supports them.

Native controls do not automatically provide infinite looping.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Overflow/Carousels
- https://developer.chrome.com/blog/new-in-web-ui-io-2025-recap
- https://www.reddit.com/r/css/comments/1ri193f/
