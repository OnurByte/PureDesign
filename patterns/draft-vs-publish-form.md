# Draft vs Publish Without Submit-Button JavaScript

## Compose

- [submitter `name` / `value`](../primitives/submitter-name-value.md)
- [`formnovalidate`](../primitives/formnovalidate.md)
- optional [`formaction` / `formmethod`](../primitives/multi-action-forms.md)

One endpoint:

```html
<form action="/documents/42" method="post">
  <input name="title" required>
  <textarea name="body" required></textarea>

  <button
    type="submit"
    name="intent"
    value="draft"
    formnovalidate>
    Save draft
  </button>

  <button
    type="submit"
    name="intent"
    value="publish">
    Publish
  </button>
</form>
```

The browser serializes the clicked submitter's intent. The server applies operation-specific validation.

## Alternative

Use `formaction` when Save Draft and Publish are cleaner as separate HTTP routes.

## Rule

Browser constraint validation is an affordance, not authority. `formnovalidate` never exempts the server from validating/authenticating the chosen operation.
