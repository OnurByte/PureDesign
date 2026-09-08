# `<dialog closedby>`

**Role:** Progressive enhancement. Treat support separately from the mature `<dialog>` element itself.

The `closedby` attribute lets HTML declare which dismissal mechanisms are allowed for a dialog.

```html
<dialog id="settings" closedby="any">
    <h2>Settings</h2>
    <button commandfor="settings" command="request-close">Close</button>
</dialog>
```

Values:

- `any` — developer controls, platform close request (for example Esc/back), and light dismiss outside the dialog
- `closerequest` — developer controls plus platform close requests
- `none` — only developer-specified mechanisms

## Replaces

A common modal implementation adds document-level pointer listeners to detect outside clicks and separate keyboard listeners for Escape.

When `closedby` is supported, the user agent can own those dismissal semantics instead.

## Why this matters

Dismissal is input-modality behavior, not merely visual state. The browser is better positioned to map desktop Escape, touch interaction, platform back/dismiss gestures, focus handling, and modal semantics consistently.

## Do not confuse this with `<dialog>` support

`<dialog>` is mature. `closedby` is newer. A browser can support dialogs while not supporting this attribute.

For conservative targets, always retain an explicit semantic close control.

```html
<form method="dialog">
    <button>Close</button>
</form>
```

or, where invoker commands are supported, a declarative close/request-close button.

## Sources

- MDN `<dialog>`: https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/dialog
- MDN `closedBy`: https://developer.mozilla.org/en-US/docs/Web/API/HTMLDialogElement/closedBy
- Small implementation/polyfill study: https://github.com/webfactory/dialog-utils
- Native drawer example using `closedby="any"`: https://github.com/ics-creative/260402_spring_animation/blob/main/examples/15_drawer.html
