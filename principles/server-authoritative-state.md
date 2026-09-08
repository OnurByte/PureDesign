# Server-Authoritative State

## Rule

Anything that changes application truth should be representable as ordinary HTTP navigation or form submission.

Examples:

- sorting and filtering -> query parameters
- pagination -> URLs
- create/update/delete -> forms
- preferences -> forms + cookie/session/account state
- authentication -> forms + server session

Example:

```text
/files?view=grid&sort=size&page=2
```

Server-rendered state can be exposed to CSS:

```html
<body data-view="grid">
```

```css
body[data-view="grid"] .files {
    display: grid;
}
```

## Why

This preserves reload, back/forward, deep links, bookmarks and authoritative server validation without a client state synchronizer.

## Constraint

Do not send trivial local UI state to the server when a browser-native primitive already owns it. Opening an accordion or menu should not require a round trip unless the interaction needs new server data.
