# `<dialog>`

**Role:** native dialog/modal semantics.

```html
<dialog id="delete-dialog">
  <p>Delete this file?</p>
</dialog>
```

The element itself is mature, but declarative invocation with `command` / `commandfor` is newer:

```html
<button commandfor="delete-dialog" command="show-modal">Delete</button>
```

## Rules

- Distinguish support for `<dialog>` from support for declarative command invocation.
- For Firefox 140 ESR/Tor targets, do not make `command="show-modal"` the only way to perform a core task.
- Do not emulate dialog semantics with a hidden checkbox merely to avoid checking browser support.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/dialog
- https://github.com/webfactory/dialog-utils
- https://github.com/picocss/pico/discussions/343
