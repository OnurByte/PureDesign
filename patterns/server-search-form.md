# Server-Rendered Search Form

## Compose

- [native search input/landmark](../primitives/search-input-and-landmark.md)
- [real forms / URL state](../principles/server-authoritative-state.md)
- optional [`autocomplete`](../primitives/autocomplete-tokens.md), [`spellcheck`](../primitives/spellcheck.md), and mobile input hints when appropriate

```html
<search>
  <form action="/files" method="get">
    <label for="q">Search files</label>
    <input id="q" type="search" name="q" value="{{ query }}">
    <button>Search</button>
  </form>
</search>
```

The result URL becomes ordinary durable navigation state:

```text
/files?q=report
```

The server renders matching results, pagination and the current query value.

## Why

No debounced `fetch()`, custom router state or search-result hydration is required for a complete baseline search experience.

Optional newer enhancement may add live suggestions, but the form submission must remain a complete path when the product contract is zero-JS.

## Privacy note

For sensitive search fields, evaluate browser spellcheck/autocomplete behavior instead of enabling every input-assistance feature by default.
