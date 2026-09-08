# `<progress>`

**Role:** semantic task-progress indicator rendered by the browser.

```html
<label for="quota-job">Encrypting files</label>
<progress id="quota-job" max="100" value="70">70%</progress>
```

Omit `value` for indeterminate progress:

```html
<progress aria-label="Processing"></progress>
```

The latter matches `:indeterminate`.

## Boundary

For a zero-JS page, the value normally changes only when the server renders a new response or navigation refreshes the state. Native `<progress>` does not magically stream live job updates.

Use it instead of a decorative `div` progress bar when the concept really is task completion progress.

## Styling

`accent-color` can provide lightweight branding while preserving native semantics.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/progress
- https://www.reddit.com/r/webdev/comments/124xx7r/
