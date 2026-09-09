# Detached Form Actions

Use this when a page wants form fields in the content area but persistent actions in a header/footer/sidebar.

## Baseline

```html
<form id="editor" action="/note/42" method="post">
  <label>
    Title
    <input name="title" required>
  </label>

  <textarea name="body"></textarea>
</form>

<footer class="action-bar">
  <button form="editor" type="submit" name="intent" value="save">
    Save
  </button>
  <button
    form="editor"
    type="submit"
    name="intent"
    value="publish"
    formaction="/note/42/publish">
    Publish
  </button>
</footer>
```

The visual layout is detached; form semantics are not.

## Why this beats click routing

- native Enter/submission behavior remains available;
- constraint validation still runs normally;
- submitter `name=value` can express intent;
- `formaction` can route an individual action;
- no client runtime is required to locate the form.

## Read

- [`../primitives/form-owner-attribute.md`](../primitives/form-owner-attribute.md)
- [`../primitives/multi-action-forms.md`](../primitives/multi-action-forms.md)
- [`../primitives/submitter-name-value.md`](../primitives/submitter-name-value.md)
- [`../primitives/native-validation.md`](../primitives/native-validation.md)
