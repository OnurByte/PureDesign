# `prefers-reduced-motion`

**Role:** let CSS respect the user's OS/browser motion preference without `matchMedia()` JavaScript.

```css
@media (prefers-reduced-motion: reduce) {
  *,
  *::before,
  *::after {
    scroll-behavior: auto;
  }

  .decorative-motion {
    animation: none;
    transition: none;
  }
}
```

## Rule

Do not merely shorten every animation mechanically. Remove/reduce motion that is unnecessary or disorienting while preserving state feedback and task comprehension.

PureDesign motion is enhancement-only anyway, so reduced-motion mode should remain fully functional.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Media_queries/Using_for_accessibility
- https://developer.mozilla.org/en-US/docs/Web/CSS/%40media/prefers-reduced-motion
