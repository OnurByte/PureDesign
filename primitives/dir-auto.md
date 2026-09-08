# `dir="auto"`

**Role:** let the browser infer base text direction for unknown/user-generated content.

```html
<p dir="auto">{{ comment }}</p>
```

The user agent determines the base direction from the first strong-direction character instead of requiring language/direction detection JavaScript.

This is especially useful for:

- chat messages;
- filenames;
- usernames/display names;
- comments;
- imported external text.

## Important

Omitting `dir` does **not** enable automatic detection; direction normally inherits from the parent. Use `dir="auto"` explicitly when content direction is unknown.

For isolated inline unknown-direction text, see [`<bdi>`](bdi.md).

## Source

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes/dir
