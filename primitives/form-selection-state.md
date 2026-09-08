# Native Selection State: `:checked`

**Role:** expose real checkbox/radio selection to CSS.

```html
<label class="option">
  <input type="radio" name="plan" value="pro">
  <span>Pro</span>
</label>
```

```css
.option:has(input:checked) {
  border-color: var(--accent);
}
```

## Use when

The state is genuinely a form selection, toggle or option that can be submitted.

## Do not use when

The hidden control is only pretending to be unrelated UI such as a modal, route or dropdown. See [`../principles/legacy-css-hacks.md`](../principles/legacy-css-hacks.md).

## Source

- https://developer.mozilla.org/en-US/docs/Web/CSS/:checked
