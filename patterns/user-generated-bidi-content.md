# Unknown-Direction User Content

## Compose

- [`dir="auto"`](../primitives/dir-auto.md)
- [`<bdi>`](../primitives/bdi.md)

For a chat/message block:

```html
<article class="message" dir="auto">
  {{ message }}
</article>
```

For an unknown-direction value embedded in surrounding prose:

```html
<p>Uploaded by <bdi>{{ username }}</bdi></p>
```

## Why

User-generated text can contain Arabic/Hebrew/Latin scripts regardless of the page locale. Let the Unicode bidi algorithm and semantic HTML own this instead of guessing language/direction in JavaScript.
