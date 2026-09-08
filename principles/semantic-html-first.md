# Semantic HTML First

## Rule

Use the element whose built-in semantics match the interaction.

Prefer:

- disclosure -> `<details>` / `<summary>`
- selection -> checkbox/radio/select
- navigation -> `<a>`
- action -> `<button>`
- data mutation -> `<form>`
- floating disclosure -> popover
- modal semantics -> `<dialog>`

## Why

Native elements already carry keyboard behavior, accessibility semantics, focus rules, submission behavior and browser state. Recreating those semantics with arbitrary elements or hidden inputs increases complexity.

## Checkbox-hack boundary

Good use:

```html
<label><input type="checkbox" name="notifications"> Notifications</label>
```

Bad default architecture:

```text
fake modal     -> hidden checkbox
fake dropdown  -> hidden checkbox
fake accordion -> hidden checkbox
fake route     -> hidden checkbox
```

Use `:checked` when the state is genuinely checkbox/radio-like, not merely because CSS can observe it.

## Test

Before building a component, ask: if author CSS disappeared, would the remaining HTML still describe the interaction honestly?
