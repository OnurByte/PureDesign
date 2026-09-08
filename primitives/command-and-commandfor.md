# `command` and `commandfor`

**Role:** Progressive enhancement. Newer than Firefox 140 ESR; do not require it for Tor Browser 15 core behavior.

Invoker commands let a real `<button>` declaratively tell another element to perform a standardized action.

```html
<button commandfor="delete-dialog" command="show-modal">
    Delete
</button>

<dialog id="delete-dialog">
    <p>Delete this file?</p>
    <button commandfor="delete-dialog" command="close">Cancel</button>
</dialog>
```

Built-in command values include dialog and popover operations such as:

- `show-modal`
- `close`
- `request-close`
- `show-popover`
- `hide-popover`
- `toggle-popover`

## Replaces

Imperative glue such as:

```text
button.addEventListener('click', ...)
 -> dialog.showModal()
 -> dialog.close()
 -> popover.showPopover()
```

for standardized browser-owned interactions.

## `request-close` vs `close`

Prefer `request-close` when the interaction should follow the platform's normal dismiss/cancel path. `close` is a direct close operation.

Do not assume custom `--commands` are zero-JS: custom commands dispatch events and normally need script to do useful work. PureDesign is interested primarily in standardized built-in commands.

## Compatibility

MDN marks the general `command` capability as Baseline 2025. Firefox added `command` / `commandfor` in Firefox 144, which is newer than the Firefox 140 ESR engine in Tor Browser 15.0.21.

Use a semantic baseline path for ESR/Tor; enable command invokers only where supported.

## Sources

- MDN button reference: https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/button
- MDN command property: https://developer.mozilla.org/en-US/docs/Web/API/HTMLButtonElement/command
- Firefox 144 release notes: https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/144
- MDN Invoker Commands source/docs: https://github.com/mdn/content/blob/main/files/en-us/web/api/invoker_commands_api/index.md
- Small progressive-enhancement project: https://github.com/webfactory/dialog-utils
