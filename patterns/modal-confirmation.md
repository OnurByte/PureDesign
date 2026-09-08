# Modal Confirmation

## Compose

- [`<dialog>`](../primitives/dialog.md)
- [`:modal` / `::backdrop`](../primitives/modal-and-backdrop-state.md)
- [`method="dialog"` / `formmethod="dialog"`](../primitives/dialog-form-method.md) for local cancel/close controls
- newer [`command` / `commandfor`](../primitives/command-and-commandfor.md)
- optional [`closedby`](../primitives/dialog-closedby.md)
- optional [`scrollbar-gutter`](../primitives/scrollbar-gutter.md) for layout stability
- ordinary form submission for the confirmed action

## Authoritative destructive action

The server endpoint is the real operation:

```html
<form action="/files/1/delete" method="post">
  <button type="submit">Delete</button>
</form>
```

A modal is only presentation/confirmation around that operation.

## Newer declarative form

```html
<button commandfor="delete-dialog" command="show-modal">Delete</button>

<dialog id="delete-dialog" closedby="any">
  <p>Delete this file?</p>

  <form action="/files/1/delete" method="post">
    <button type="submit">Confirm delete</button>
    <button type="submit" formmethod="dialog">Cancel</button>
  </form>
</dialog>
```

The browser can own modal/top-layer state, the backdrop and local dialog dismissal. `formmethod="dialog"` closes the dialog without sending the destructive POST; the confirmation button still uses the real server endpoint.

## Compatibility rule

For Tor Browser / Firefox 140 ESR, do not make newer declarative dialog commands the only route to a critical task. `command/commandfor` landed in Firefox 144.

The underlying destructive action must remain a server-valid form endpoint, and the critical workflow needs a baseline route that does not depend on newer invoker commands.
