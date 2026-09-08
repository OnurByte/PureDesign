# Findable Collapsed Content

## Compose

- [`hidden="until-found"`](../primitives/hidden-until-found.md)

Use when content should be visually collapsed by default but still discoverable through browser Find in Page or a direct fragment.

```html
<section id="advanced" hidden="until-found">
  <h2>Advanced settings</h2>
  ...
</section>
```

## Good uses

- long settings screens
- reference/help pages
- archived detail blocks

## Rule

Do not apply global `[hidden] { display:none !important; }` resets that erase `until-found` semantics.
