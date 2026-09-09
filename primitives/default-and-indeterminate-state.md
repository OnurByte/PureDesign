# `:default` and `:indeterminate`

**Role:** expose additional browser-owned form/control states without custom classes.

## `:default`

Matches the default option/control in a set, even after current user state changes.

```html
<label>
  <input type="radio" name="sort" value="name" checked>
  Name
</label>
```

```css
input:default + .label::after {
  content: " (default)";
}
```

This can show the original/default choice without a `.was-default` class.

## `:indeterminate`

Matches controls with no determinate state.

Useful zero-JS cases include:

- `<progress>` with no `value` attribute;
- a same-named radio group before any radio is selected.

```css
progress:indeterminate {
  opacity: .75;
}
```

A checkbox's `indeterminate` state generally requires its DOM property to be set programmatically, so do **not** claim CSS alone can create tri-state checkbox behavior.

## Source

- https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Forms/UI_pseudo-classes
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/progress
