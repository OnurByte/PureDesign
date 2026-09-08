# Selectable Cards

## Compose

- real radio/checkbox state
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
