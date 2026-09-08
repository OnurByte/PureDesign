# `method="dialog"` / `formmethod="dialog"`

**Role:** close a dialog through native form semantics without an HTTP request or `preventDefault()` script.

```html
<dialog id="preferences">
  <form method="dialog">
    <label>
      Sort
      <select name="sort">
        <option>name</option>
        <option>size</option>
      </select>
    </label>

    <button value="cancel">Cancel</button>
    <button value="confirm">Confirm</button>
  </form>
</dialog>
```

When submitted with the `dialog` method, the browser closes the dialog, preserves the control state and does not submit the form over the network. The activated submitter's value becomes the dialog return value for scripting environments.

A single submitter can override another form method:

```html
<button formmethod="dialog">Cancel</button>
```

## Boundary

This is for local dialog completion/dismissal. If an action must mutate server state, submit a real `POST` form endpoint instead.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/dialog
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/form
