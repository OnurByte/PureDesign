# Long server-rendered list without client virtualization

## Goal

Keep a large server-rendered file/message/feed list responsive without introducing a client rendering runtime merely to skip off-screen paint/layout work.

## First: bound the dataset on the server

Use real pagination/cursors:

```text
/messages?page=4
/files?cursor=...
```

Do not send an unbounded database table just because CSS can skip rendering.

## Then: let the browser skip off-screen rendering

```css
.list-item {
    content-visibility: auto;
    contain-intrinsic-size: auto 76px;
}
```

Choose the intrinsic estimate from realistic row dimensions.

## What this gains

The HTML remains:

- server-rendered
- Find-in-Page accessible
- keyboard reachable
- semantically present

while the browser can skip layout/paint work for off-screen rows.

## What it does not gain

This is not equivalent to a fully virtualized data grid. It does not reduce DOM node count or response bytes.

Architecture:

```text
DB/result size       -> server pagination
HTML generation      -> server
DOM semantics        -> complete returned page
visible render work  -> browser content-visibility
```

## Read

- [`../primitives/content-visibility.md`](../primitives/content-visibility.md)
- [`server-filter-sort-pagination.md`](server-filter-sort-pagination.md)
- [`../principles/server-authoritative-state.md`](../principles/server-authoritative-state.md)
