# Customizable Native `<select>`

**Role:** keep real select semantics while allowing much richer native picker styling in supporting browsers.

```css
select,
select::picker(select) {
  appearance: base-select;
}
```

Related newer pieces include:

- `::picker(select)`
- `::picker-icon`
- `::checkmark`
- `:open`
- `:checked`
- `<selectedcontent>`

## Fallback contract

```text
supports base-select -> branded picker
unsupported          -> ordinary native select
```

Do not replace the real `<select>` merely to gain styling.

Firefox 140 ESR cannot treat this styling model as core behavior.

## Sources

- https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Forms/Customizable_select
- https://gist.github.com/ijurko
- https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/149
- https://github.com/sveltejs/svelte/issues/18347
- https://github.com/solidjs/solid/discussions/2463
