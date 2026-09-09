# `formnovalidate`

**Role:** let one submit action bypass browser constraint validation without JavaScript.

Typical server-rendered editor:

```html
<form action="/drafts/42" method="post">
  <input name="title" required>
  <textarea name="body" required></textarea>

  <button type="submit">Publish</button>
  <button
    type="submit"
    name="intent"
    value="draft"
    formnovalidate>
    Save draft
  </button>
</form>
```

`Publish` uses normal constraint validation. `Save draft` may submit incomplete fields.

## What this replaces

A click handler that temporarily disables validation or manually calls submission APIs depending on which button was clicked.

## Boundary

`formnovalidate` bypasses **browser constraint validation only**.

The server must still validate according to the chosen operation. A draft endpoint may accept incomplete data while publish requires stronger invariants.

Do not use this to bypass security validation.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/button
- https://developer.mozilla.org/en-US/docs/Web/API/HTMLButtonElement/formNoValidate
