# Accordion

## Use

FAQ, settings groups, expandable metadata.

## Compose

- [`<details>` / `<summary>`](../primitives/details.md)
- optional [`@starting-style` / discrete transitions](../primitives/starting-style-and-discrete-transitions.md)

## Baseline

```html
<details name="settings">
  <summary>Security</summary>
  <div class="panel">...</div>
</details>

<details name="settings">
  <summary>Storage</summary>
  <div class="panel">...</div>
</details>
```

## Rules

- Do not use hidden checkbox state when `<details>` matches the semantics.
- Animation is optional.
- Test long panels on mobile; grouped auto-close behavior can shift scroll position.
