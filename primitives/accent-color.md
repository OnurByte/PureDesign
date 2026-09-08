# `accent-color`

**Role:** brand native controls without rebuilding them.

```css
:root {
  accent-color: var(--accent);
}
```

Browsers currently apply it to controls including:

- checkbox;
- radio;
- range;
- progress.

## Why

A common reason native controls get replaced with custom JavaScript widgets is visual mismatch. `accent-color` gives a low-cost branding layer while retaining browser behavior and accessibility.

Do not expect complete visual control; the user agent still owns the control.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/accent-color
- https://www.reddit.com/r/webdev/comments/124xx7r/
