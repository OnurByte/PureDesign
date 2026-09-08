# Multi-Action Form

## Compose

- [native multi-action form attributes](../primitives/multi-action-forms.md)
- [native validation](../primitives/native-validation.md)

Use one form with multiple native submitters instead of attaching click handlers.

```html
<form action="/drafts/save" method="post">
  <input name="title" required>

  <button type="submit">Save draft</button>
  <button type="submit" formaction="/drafts/publish">Publish</button>
  <button type="submit" formaction="/drafts/preview" formmethod="get">Preview</button>
</form>
```

## Good uses

- Save / Save and close
- Draft / Publish
- Search / Export
- Preview through GET

Each server endpoint remains explicit and independently valid.
