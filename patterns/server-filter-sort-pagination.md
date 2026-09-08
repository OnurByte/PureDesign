# Server-Rendered Filter / Sort / Pagination

## Compose

- [server-authoritative state](../principles/server-authoritative-state.md)
- ordinary links/forms
- optional CSS state rendered from server attributes

Example URL:

```text
/files?view=grid&sort=size&page=2
```

Example form:

```html
<form action="/files" method="get">
  <select name="sort">
    <option value="name">Name</option>
    <option value="size">Size</option>
  </select>
  <button type="submit">Apply</button>
</form>
```

Server response can expose state:

```html
<body data-view="grid" data-sort="size">
```

## Benefits

- bookmarkable
- reload-safe
- back/forward-safe
- shareable
- server remains authoritative

Do not rebuild query state in a client store when normal URLs already model it correctly.
