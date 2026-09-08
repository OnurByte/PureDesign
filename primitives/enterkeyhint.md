# `enterkeyhint`

**Role:** tell the virtual keyboard what action the Enter key represents.

```html
<input
  type="search"
  name="q"
  enterkeyhint="search">
```

Common values include:

- `enter`
- `done`
- `go`
- `next`
- `previous`
- `search`
- `send`

The browser/IME chooses the actual localized label or icon.

## Why

Do not use device-detection JavaScript just to relabel the virtual keyboard action. This is presentation/input affordance owned by the browser.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes/enterkeyhint
