# Native Form Validation

**Role:** browser-owned constraint state and validation feedback.

```html
<label class="field">
  <span>Email</span>
  <input type="email" name="email" required>
</label>
```

Prefer user-triggered validation styling:

```css
input:user-invalid { border-color: var(--danger); }
input:user-valid { border-color: var(--success); }
```

Combined with `:has()`:

```css
.field:has(input:user-invalid) { border-color: var(--danger); }
```

## Rule

Server-side validation remains authoritative. Native validation is client-side affordance, not trust boundary.

`:user-invalid` is often better than painting all untouched required fields as errors with `:invalid`.

## Sources

- https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Forms/Form_validation
- https://www.reddit.com/r/css/comments/1oasqw0/
