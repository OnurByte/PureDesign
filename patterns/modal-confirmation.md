# Modal Confirmation

## Compose

- [`<dialog>`](../primitives/dialog.md)
- ordinary form submission for the confirmed action

```html
<dialog id="delete-dialog">
  <p>Delete this file?</p>

  <form action="/files/1/delete" method="post">
    <button type="submit">Delete</button>
  </form>
</dialog>
```

Supporting newer browsers may use declarative `command` / `commandfor` to open and close the dialog.

## Compatibility rule

For Tor Browser / Firefox 140 ESR, do not make newer declarative dialog commands the only route to a critical task. The underlying destructive action must remain a server-valid form endpoint.
