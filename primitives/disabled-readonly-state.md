# `disabled` / `readonly` / `:disabled` / `:read-only`

These states are not interchangeable.

## `disabled`

Disabled controls:

- are not interactive;
- normally cannot receive focus;
- are not submitted with the form;
- match `:disabled`.

## `readonly`

Read-only controls remain focusable and are still submitted, but the user cannot edit them.

```html
<input name="username" value="alice" readonly>
<input name="internal" value="x" disabled>
```

```css
:disabled { opacity: .55; }
:read-only { background: var(--surface-muted); }
```

Do not replace semantic disabled/read-only state with `.disabled` styling plus click guards.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/disabled
- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/Pseudo-classes
