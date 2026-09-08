# Selectable Cards

## Compose

- [native checkbox/radio selection state](../primitives/form-selection-state.md)
- [`:has()`](../primitives/has.md)

```html
<label class="plan">
  <input type="radio" name="plan" value="pro">
  <span>Pro</span>
</label>
```

```css
.plan:has(input:checked) {
  border-color: var(--accent);
  background: var(--selected-bg);
}
```

## State ownership

Selection -> real form control. Card appearance -> CSS.

Do not turn a `<div>` into a fake selectable state machine when the submitted value is genuinely radio/checkbox state.
