# Multi-Action Form

## Compose

- [native multi-action form attributes](../primitives/multi-action-forms.md)
- [submitter `name` / `value`](../primitives/submitter-name-value.md)
- [`formnovalidate`](../primitives/formnovalidate.md) where one action intentionally permits incomplete browser-validity state
- [native validation](../primitives/native-validation.md)

Use one form with multiple native submitters instead of attaching click handlers.

## Separate routes

```html
<form action="/drafts/save" method="post">
  <input name="title" required>

  <button type="submit">Save</button>
  <button type="submit" formaction="/drafts/publish">Publish</button>
  <button type="submit" formaction="/drafts/preview" formmethod="get">Preview</button>
</form>
```

## Same route, explicit intent

```html
<form action="/drafts/42" method="post">
  <input name="title" required>

  <button name="intent" value="draft" formnovalidate>Save draft</button>
  <button name="intent" value="publish">Publish</button>
</form>
```

The clicked successful submitter contributes its `name=value` pair to the request. The browser owns submitter selection; the server owns the meaning, validation and authorization of the requested action.

## Good uses

- Save / Save and close
- Draft / Publish
- Search / Export
- Preview through GET

No click-routing JavaScript is required.
