# Declarative dialog drawer

## Goal

Build a side drawer / mobile navigation panel using browser modal state instead of client event listeners.

## New-browser form

```html
<button commandfor="drawer" command="show-modal">
    Open menu
</button>

<dialog id="drawer" class="drawer" closedby="any">
    <nav aria-label="Main navigation">
        <a href="/files">Files</a>
        <a href="/settings">Settings</a>
    </nav>

    <button commandfor="drawer" command="request-close">
        Close
    </button>
</dialog>
```

```css
.drawer {
    inset: 0 0 0 auto;
    margin: 0;
    block-size: 100dvh;
    inline-size: min(26rem, 92vw);
    max-block-size: none;
    max-inline-size: none;
    overflow: auto;
    overscroll-behavior: contain;
}

.drawer::backdrop {
    background: rgb(0 0 0 / .35);
}
```

## Browser ownership

```text
modal/top-layer state -> dialog
open/close command     -> command/commandfor
Esc/back/light dismiss -> closedby/platform
background inertness   -> modal dialog semantics
backdrop               -> ::backdrop
scroll containment     -> overscroll-behavior
```

## Conservative baseline

`command/commandfor` is newer than Firefox 140 ESR. If Tor/ESR is core, use a navigation/disclosure baseline that works there and treat the dialog drawer as a newer-browser enhancement, or render the navigation as an always-available server page.

Do not add a JavaScript polyfill and still call the result zero-client-JS.

## Read

- [`../primitives/dialog.md`](../primitives/dialog.md)
- [`../primitives/command-and-commandfor.md`](../primitives/command-and-commandfor.md)
- [`../primitives/dialog-closedby.md`](../primitives/dialog-closedby.md)
- [`../primitives/overscroll-behavior.md`](../primitives/overscroll-behavior.md)
- [`../primitives/scrollbar-gutter.md`](../primitives/scrollbar-gutter.md)
