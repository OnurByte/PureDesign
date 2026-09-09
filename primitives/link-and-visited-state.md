# Link and Visited State

**Role:** style real navigation links according to browser-owned link/history state.

```css
a:any-link {
  text-underline-offset: .18em;
}

a:visited {
  color: var(--visited-link);
}
```

`:link` matches unvisited links and `:visited` matches links present in browser history.

## Privacy boundary

Visited history is intentionally protected from applications.

Browsers restrict `:visited` styling mostly to color-related properties and deliberately prevent JavaScript/selector APIs from learning a user's browsing history through computed style or selector matching.

Therefore:

```text
visited link state -> browser-private presentation state
application read/unread state -> server/application data
```

Do **not** use `:visited` to represent whether a notification, message, file, or application record has been read. Those are durable application states and belong on the server.

## Ordering

When specificity is equal, conventional link state ordering is:

```text
:link -> :visited -> :hover -> :active
```

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/:visited
- https://developer.mozilla.org/en-US/docs/Web/CSS/Privacy_and_the_:visited_selector
