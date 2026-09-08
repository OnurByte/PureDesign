# `:autofill`

**Role:** style browser-owned autofill state without reading field values in JavaScript.

```css
input:autofill {
  outline: 2px solid var(--autofill-ring);
}
```

Firefox enabled `:autofill` in Firefox 86, with `:-webkit-autofill` kept as an alias for compatibility.

## Why it matters

Autofill is a browser/password-manager interaction state. Scripts that infer whether a field is filled by checking `.value` can be unreliable around autofill and password-manager behavior.

## Rules

- Use valid `autocomplete` tokens so the browser understands field purpose.
- Do not broadly disable autofill just to simplify styling.
- Test autofill together with floating labels / `:placeholder-shown`.

## Sources

- https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/86
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/autocomplete
- https://www.reddit.com/r/web_design/comments/u3hrbz/
