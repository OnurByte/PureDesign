# `<meter>`

**Role:** semantic scalar measurement inside a known range.

Use for quota usage, disk fullness, signal quality, score bands, or other measurements — not for task progress.

```html
<label for="storage">Storage used</label>
<meter id="storage" min="0" max="100" low="60" high="85" optimum="20" value="72">
  72%
</meter>
```

`low`, `high`, and `optimum` let the browser understand which portions of the range are desirable.

## Difference from `<progress>`

- `<progress>` = completion of a task.
- `<meter>` = current value within a known range.

Do not rebuild either as meaningless `<div>` elements merely for styling convenience.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/meter
- https://www.reddit.com/r/webdev/comments/124xx7r/
