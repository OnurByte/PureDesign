# `autocomplete` Tokens

**Role:** communicate field purpose to the browser/password manager so autofill can work without custom value-restoration JavaScript.

```html
<input name="email" type="email" autocomplete="email">
<input name="name" autocomplete="name">
<input name="new-password" type="password" autocomplete="new-password">
```

For one-time codes:

```html
<input
  name="otp"
  inputmode="numeric"
  autocomplete="one-time-code">
```

## Rules

- Use the specific standardized token that represents the actual field purpose.
- Do not disable autocomplete globally merely to simplify styling/state logic.
- Treat password-manager/autofill behavior as browser-owned state and test it together with `:autofill` and floating-label styles.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/autocomplete
