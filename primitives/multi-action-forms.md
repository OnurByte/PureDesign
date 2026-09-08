# Multi-Action Native Forms

**Role:** route different submit buttons to different endpoints/methods without click handlers.

```html
<form id="file-form" action="/files/save" method="post">
  <input name="name" required>

  <button type="submit">Save</button>

  <button type="submit" formaction="/files/save-and-close">
    Save and close
  </button>

  <button
    type="submit"
    formaction="/files/preview"
    formmethod="get"
    formtarget="_blank">
    Preview
  </button>
</form>
```

A submit button can also live outside the form:

```html
<form id="profile" action="/profile" method="post">...</form>
<footer><button form="profile" type="submit">Save profile</button></footer>
```

## Replaces

```text
click listener -> inspect button -> choose endpoint -> fetch()
```

with native submitter semantics and ordinary HTTP.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/button
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/form
