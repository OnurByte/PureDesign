# Mobile-Friendly Form Without Device Detection

## Compose

- [`inputmode`](../primitives/inputmode.md)
- [`enterkeyhint`](../primitives/enterkeyhint.md)
- [`autocomplete`](../primitives/autocomplete-tokens.md)
- normal semantic input types and constraints

```html
<form action="/login" method="post">
  <label>
    Email
    <input
      type="email"
      name="email"
      autocomplete="email"
      inputmode="email"
      enterkeyhint="next"
      required>
  </label>

  <label>
    Password
    <input
      type="password"
      name="password"
      autocomplete="current-password"
      enterkeyhint="done"
      required>
  </label>

  <button type="submit">Sign in</button>
</form>
```

## Rule

Describe the field's semantics to the browser. Do not detect iPhone/Android/desktop merely to change keyboards, autofill or Enter-key affordances.
