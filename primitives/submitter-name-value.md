# Submitter `name` / `value`

**Role:** let the clicked submit button tell the server which action the user chose without click-handler JavaScript.

```html
<form action="/document/42" method="post">
  <input name="title" required>

  <button type="submit" name="intent" value="save">Save</button>
  <button type="submit" name="intent" value="publish">Publish</button>
</form>
```

The successful submitter contributes its own name/value pair to form data:

```text
intent=save
```

or:

```text
intent=publish
```

The server can branch on `intent` while keeping one endpoint.

## Use with

- [`multi-action-forms.md`](multi-action-forms.md) when different buttons need different endpoints/methods.
- `formaction` when actions are cleaner as separate routes.

## Boundary

The browser identifies the submitter and serializes form data. The server owns the meaning and authorization of the requested action.

Never trust the submitted `intent` as authorization.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/button
- https://developer.mozilla.org/en-US/docs/Web/API/HTMLFormElement/requestSubmit
