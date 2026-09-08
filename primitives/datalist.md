# `<datalist>`

**Role:** browser-managed suggestions/autocomplete for simple inputs.

```html
<label for="city">City</label>
<input id="city" name="city" list="cities">

<datalist id="cities">
  <option value="Bolu">
  <option value="Ankara">
  <option value="Istanbul">
</datalist>
```

## Use when

Suggestions are optional and browser-native styling/behavior is acceptable.

## Do not assume

`<datalist>` is not a universal replacement for a sophisticated accessible combobox. Styling, value/display relationships and assistive-technology behavior have limitations across implementations.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/datalist
- https://www.reddit.com/r/webdev/comments/brnwj9/
