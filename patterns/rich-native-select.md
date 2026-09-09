# Rich native select

## Goal

Build a currency, language, account or similar rich picker while keeping real `<select>` semantics and an ordinary native-select fallback.

## Compose

- [native select](../primitives/native-select.md)
- [customizable native select](../primitives/customizable-select.md)
- [`:open`](../primitives/open-pseudo-class.md)

## Baseline

The control is still a real select with real option values:

```html
<label for="currency">Currency</label>
<select id="currency" name="currency">
  <button>
    <selectedcontent></selectedcontent>
  </button>

  <option value="eur">
    <span aria-hidden="true">€</span>
    <span>EUR — Euro</span>
  </option>
  <option value="gbp">
    <span aria-hidden="true">£</span>
    <span>GBP — British pound</span>
  </option>
  <option value="usd" selected>
    <span aria-hidden="true">$</span>
    <span>USD — US dollar</span>
  </option>
</select>
```

The first child `<button>` hosts `<selectedcontent>`, which mirrors the selected option in supporting customizable-select implementations. The selected value still submits through the native select.

## Progressive styling

```css
@supports (appearance: base-select) {
  #currency,
  #currency::picker(select) {
    appearance: base-select;
  }

  #currency option {
    display: grid;
    grid-template-columns: 2rem 1fr;
    gap: .5rem;
    align-items: center;
  }

  #currency option:checked {
    font-weight: 700;
  }
}
```

Use `::picker(select)`, `::picker-icon`, `::checkmark`, `:open` and `:checked` only as presentation enhancements. Do not replace the select with a fake listbox just to gain styling.

## Fallback contract

```text
customizable select supported -> rich picker presentation
unsupported                    -> ordinary native select behavior
submitted value                -> native select in both cases
```

Keep critical option meaning in text. Icons, symbols or images must not be the only way to identify an option.

## Tor / ESR

Firefox 140 ESR / Tor Browser 15 cannot make the customizable-select styling model core behavior. The ordinary native select remains the required path.

## Research provenance

- https://github.com/Annie-Huang/currency-picker-customizable-select — small example using `<selectedcontent>` and rich currency options.
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/selectedcontent
- https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Forms/Customizable_select
