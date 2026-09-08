# `inputmode`

**Role:** hint the appropriate virtual keyboard without device-detection JavaScript.

```html
<input
  name="amount"
  inputmode="decimal"
  autocomplete="off">
```

Useful values include `text`, `decimal`, `numeric`, `tel`, `search`, `email`, `url`, and `none`.

## Important boundary

`inputmode` changes the keyboard hint, **not validation semantics**. If the value really is an email address, URL, number, etc., use the appropriate input type/constraints where their behavior matches the product.

Do not sniff mobile user agents merely to swap keyboard layouts.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes/inputmode
