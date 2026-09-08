# Native `<select>`

**Role:** browser-owned single/multiple option selection.

```html
<label>
  Sort by
  <select name="sort">
    <optgroup label="Metadata">
      <option value="name">Name</option>
      <option value="size">Size</option>
    </optgroup>
    <option value="updated">Updated</option>
  </select>
</label>
```

Use the real control before implementing a div-based custom dropdown. The browser owns keyboard navigation, platform picker behavior, focus, selection state and form serialization.

Useful native features:

- `<optgroup>` for grouped choices;
- `multiple` for multi-selection;
- `size` for a list-box presentation;
- `required` for constraint validation;
- selected state through `<option selected>` / form submission.

## Styling boundary

Traditional `<select>` styling is intentionally limited. Limited styling is not, by itself, sufficient reason to throw away native semantics. For newer richer styling, see [Customizable Select](customizable-select.md) as progressive enhancement.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/select
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/optgroup
