# `popovertargetaction`

**Role:** Stable declarative Popover control where the Popover API baseline is supported.

A popover invoker does not have to be a simple toggle. `popovertargetaction` can explicitly show, hide, or toggle a target popover.

```html
<button popovertarget="filters" popovertargetaction="show">
    Open filters
</button>

<div id="filters" popover="manual">
    <form action="/search" method="get">
        <!-- filters -->
        <button>Apply</button>
    </form>

    <button popovertarget="filters" popovertargetaction="hide">
        Cancel
    </button>
</div>
```

Allowed values:

- `show`
- `hide`
- `toggle` (default when omitted)

## Replaces

Separate click handlers whose only job is calling:

```text
showPopover()
hidePopover()
togglePopover()
```

## Why keep this separate from `command` / `commandfor`

`popovertarget` / `popovertargetaction` are Popover-specific and landed earlier. Generic invoker commands are a newer abstraction that can also control dialogs and other standardized command targets.

For a conservative browser baseline, the older Popover-specific attributes may be available when generic `command` / `commandfor` are not.

## Firefox/Tor relevance

Firefox 125 added Popover support including `popovertarget` and `popovertargetaction`. Therefore they exist in the Firefox 140 ESR engine baseline used by Tor Browser 15.0.21, subject to Tor-specific testing.

## Sources

- MDN Popover usage: https://developer.mozilla.org/en-US/docs/Web/API/Popover_API/Using
- MDN button API: https://developer.mozilla.org/en-US/docs/Web/API/HTMLButtonElement/popoverTargetAction
- Firefox 125 release notes: https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/125
