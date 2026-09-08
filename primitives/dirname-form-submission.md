# `dirname` Form Submission

**Role:** submit the browser-determined directionality of user-entered text alongside its value.

```html
<textarea
  name="comment"
  dir="auto"
  dirname="comment-direction"></textarea>
```

A normal form submission can include both:

```text
comment=...
comment-direction=ltr|rtl
```

This lets a server persist how the user/browser interpreted the text direction without client-side language or bidi-detection JavaScript.

## Use

Useful for user-generated content that will later be rendered in mixed LTR/RTL contexts.

## Compatibility

MDN marks `dirname` as widely available since 2023. It applies to `<textarea>` and several text-like input types.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/dirname
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes/dir
