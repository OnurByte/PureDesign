# `focusgroup`

**Role:** emerging declarative roving focus / arrow-key navigation for composite groups.

```html
<div focusgroup="toolbar wrap" aria-label="Editor actions">
  <button>Bold</button>
  <button>Italic</button>
  <button>Underline</button>
</div>
```

The user agent can own arrow-key movement, group entry, focus memory, wrapping and axis behavior.

## Important boundary

`focusgroup` owns keyboard focus movement, not application selection state.

```text
keyboard navigation -> browser
selected item       -> form/URL/server/native selection control
```

Treat this as future/enhancement-only for Tor Browser / Firefox ESR targets.

## Sources

- https://developer.chrome.com/blog/new-in-chrome-150
- https://github.com/whatwg/html/issues/11641
- https://github.com/MicrosoftEdge/Demos/blob/main/focusgroup/tablist.html
- https://github.com/whatwg/html/issues/12776
