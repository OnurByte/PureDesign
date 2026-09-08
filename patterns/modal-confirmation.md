# Modal Confirmation

## Compose

- [`<dialog>`](../primitives/dialog.md)
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
  </form>

  <button commandfor="delete-dialog" command="request-close">Cancel</button>
</dialog>
```

The browser can own modal/top-layer state, platform close requests, and (where `closedby="any"` is supported) light dismissal.

## Compatibility rule

For Tor Browser / Firefox 140 ESR, do not make newer declarative dialog commands the only route to a critical task. `command/commandfor` landed in Firefox 144.

The underlying destructive action must remain a server-valid form endpoint, and the critical workflow needs a baseline route that does not depend on newer invoker commands.
