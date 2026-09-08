# State Ownership

## Rule

Put each kind of state where it naturally belongs.

```text
Ephemeral interaction state -> browser-native HTML state
Form state                  -> native form controls
Navigation state            -> URL
Durable application state   -> server
Visual state                -> CSS
Client-side JS              -> 0
```

## Browser-owned state

Examples:

- `<details open>`
- `:popover-open`
- `:checked`
- `:focus-visible`
- `:focus-within`
- `:user-invalid`
- `:target`

CSS should derive presentation from these states instead of requiring JavaScript to add/remove classes.

## Server-owned state

Sorting, filtering, CRUD, authentication, authorization, pagination, search, uploads, preferences and other authoritative state should survive a reload and therefore belong in URLs, forms, cookies/session state, or persisted server state.

## Decision test

Ask:

1. Must this state survive reload/back/forward/share?
2. Is there already a semantic browser primitive that owns it?
3. Is it merely a visual consequence of another state?

If it is durable, prefer server/URL state. If it is ephemeral and browser-native, let the browser own it. If it is visual, derive it in CSS.
