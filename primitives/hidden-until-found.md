# `hidden="until-found"`

**Role:** hide content while keeping it discoverable by Find in Page and fragment navigation.

```html
<section id="advanced-settings" hidden="until-found">
  <h2>Advanced settings</h2>
  <p>Rarely used settings...</p>
</section>
```

The browser may reveal the content when text search or a fragment targets it.

## Good uses

- advanced settings
- archived/help sections
- collapsed reference material
- dense documentation

## Footgun

Do not destroy the behavior with a generic reset:

```css
[hidden] { display: none !important; }
```

Safer:

```css
[hidden]:where(:not([hidden="until-found"])) {
  display: none !important;
}
```

Firefox added support in Firefox 139, making it relevant to a Firefox 140 ESR baseline.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes/hidden
- https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/139
- https://gist.github.com/vic876vb/cb113ea7eac166c566b21714d53fa9c4
