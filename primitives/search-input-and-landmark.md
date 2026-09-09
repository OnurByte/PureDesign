# Native Search Input and Landmark

**Role:** express search semantics and normal query submission without custom searchbox JavaScript.

Baseline server search:

```html
<search>
  <form action="/files" method="get">
    <label for="file-search">Search files</label>
    <input id="file-search" type="search" name="q">
    <button>Search</button>
  </form>
</search>
```

If `<search>` is not desired, a form may use `role="search"`:

```html
<form role="search" action="/files" method="get">
  ...
</form>
```

`<input type="search">` behaves like a text field intended for search and may receive browser-specific search UI such as a clear affordance or search-oriented virtual keyboard action.

## State ownership

Query text -> native form control.

Search request -> URL/HTTP GET.

Results -> server-rendered response.

Search landmark -> `<search>` or `role="search"`.

## Compatibility

Firefox added `<search>` in Firefox 118, so it predates the Firefox 140 ESR baseline.

## Rules

- Give the search input an accessible label.
- Give the input a `name`, otherwise its value is not submitted.
- Search results themselves belong in main content, not inside `<search>` merely because they are results.
- Do not build a custom `contenteditable role=searchbox` when a normal search input fits.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input/search
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/search
- https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Reference/Roles/search_role
- https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/118
