# Legacy CSS Hacks

## Purpose

Older no-JS UI often uses hidden checkboxes/radios plus sibling selectors as a generic state machine. These techniques are useful history and sometimes valid, but they should not be PureDesign's default when modern semantic primitives exist.

## Typical shape

```html
<input id="menu-state" type="checkbox" hidden>
<label for="menu-state">Menu</label>
<div class="menu">...</div>
```

```css
#menu-state:not(:checked) ~ .menu { display: none; }
```

## Why this can be wrong

A checkbox has checkbox semantics. If it is actually acting as a modal, dropdown, tab or disclosure, keyboard/accessibility behavior can diverge from the visual component.

Prefer:

```text
disclosure -> details/summary
menu/panel -> popover
selection  -> real checkbox/radio/select
URL state  -> :target or server URL state
modal      -> dialog where the target invocation path is supported
```

## When checkbox/radio state is appropriate

When the UI genuinely represents form selection or a persistent on/off option. In that case `:checked` plus `:has()` is clean and semantic.

## Historical/reference sources

- https://github.com/bk/aveccss/
- https://github.com/z29591259/CssTrick
- https://www.reddit.com/r/webdev/comments/10gpdxn/
- https://github.com/bilal-23/no-js — useful caution: a repository named “no-js” may still use JavaScript for components; inspect the actual contract rather than the name.
