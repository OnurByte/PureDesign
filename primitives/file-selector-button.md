# `::file-selector-button`

**Role:** style the browser's real file-picker button instead of replacing it with a fake button plus click forwarding.

```css
input[type="file"]::file-selector-button {
  font: inherit;
  padding: .6rem .9rem;
  border: 1px solid var(--border);
  border-radius: .5rem;
  background: var(--surface);
}
```

Firefox supports the standard pseudo-element since Firefox 82.

## Boundary

The filename / “no file chosen” text beside the button is still largely user-agent controlled. Accept that limitation unless the product genuinely needs a custom uploader.

## Sources

- https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/82
- https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Forms/Advanced_form_styling
- https://www.reddit.com/r/css/comments/1b80vyz/
