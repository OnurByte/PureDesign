# Server Streaming Without Patch JavaScript — Future Pattern

## Compose

- [Declarative Partial Updates](../primitives/declarative-partial-updates.md)

## Goal

Stream a page shell immediately, allow slow server components to finish later, and patch their HTML into place without shipping inline client patch scripts.

Conceptual flow:

```text
server sends shell
 -> browser renders
 -> slow component finishes
 -> <template for> patch arrives
 -> browser patches DOM
```

## Status

Research/watchlist only. This is not a Firefox 140 ESR / Tor Browser production pattern yet.

## Why keep it

It is directly relevant to zero-client-JS server frameworks because it attacks one of the remaining reasons SSR systems inject JavaScript during streaming.
