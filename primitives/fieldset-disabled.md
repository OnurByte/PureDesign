# `<fieldset disabled>`

**Role:** disable a whole related form-control group with one semantic attribute.

```html
<fieldset disabled>
  <legend>Billing details</legend>
  <input name="card-number">
  <input name="expiry">
</fieldset>
```

All descendant form controls are disabled except controls inside the `<legend>`.

## Replaces

```text
querySelectorAll(inputs)
 -> loop
 -> control.disabled = true
```

when the server already knows that the whole group is unavailable.

## Important

Disabled descendants are not submitted. If values must still be submitted, `readonly` or another architecture may be appropriate instead.

Use `<legend>` to label the group.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/fieldset
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/disabled
