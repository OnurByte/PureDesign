# Validation Feedback

## Compose

- [native constraint validation](../primitives/native-validation.md)
- [`:has()`](../primitives/has.md)
- server-side validation as authority

```html
<label class="field">
  <span>Email</span>
  <input type="email" name="email" required>
</label>
```

```css
.field:has(input:user-invalid) {
  border-color: var(--danger);
}
```

## Rule

Prefer feedback after meaningful user interaction instead of styling every initially empty required input as an error.

Native validation improves interaction; the server still validates all submitted data.
