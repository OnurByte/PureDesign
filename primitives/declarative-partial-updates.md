# Declarative Partial Updates (`<template for>`)

**Role:** emerging native out-of-order HTML patching for streamed server rendering without inline patch scripts.

Conceptual model:

```html
<div id="results">
  <?start name="results">Loading…<?end>
</div>

<template for="results">
  <article>Result One</article>
</template>
```

## Why it matters

Today a slow server component usually means either:

```text
block whole response
```

or:

```text
stream placeholder -> inline JS patches DOM later
```

The proposed model is:

```text
stream shell
 -> slow component completes
 -> declarative patch arrives
 -> browser applies patch
```

This could bring out-of-order server streaming to a zero-client-JS architecture.

## Status

Experimental/future-facing. Do not use as a Tor/Firefox ESR production assumption. Other proposal directions include same-document navigation and native fragment inclusion ideas.

## Historical precursor

PHOOOS explored Declarative Shadow DOM for a similar no-JS out-of-order streaming problem before a cleaner platform primitive was proposed.

## Sources

- https://developer.chrome.com/docs/web-platform/declarative-partial-updates
- https://github.com/WICG/declarative-partial-updates
- https://github.com/WICG/declarative-partial-updates/blob/main/patching-explainer.md
- https://www.reddit.com/r/webdev/comments/1bq9l84/
- https://www.reddit.com/r/webdev/comments/1c9jgzw/
- https://www.reddit.com/r/webdev/comments/1tma96z/
