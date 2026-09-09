# Explicit Form Ownership with `form`

**Role:** associate a native form control with a form elsewhere in the same document.

This is useful when layout and form ownership should not be forced to match.

```html
<form id="profile" action="/profile" method="post">
  <label>
    Display name
    <input name="display_name" required>
  </label>
</form>

<footer class="sticky-actions">
  <button form="profile" type="submit">Save</button>
</footer>
```

The footer button is still a real submit button for `#profile`. No click handler, DOM lookup or request-building code is needed.

## Supported elements

The HTML `form` attribute applies to form-associated elements including `button`, `fieldset`, `input`, `object`, `output`, `select` and `textarea`.

## Important boundary

`form` is **not inherited**. Setting it on a `fieldset` does not automatically associate every descendant control with that form.

```html
<form id="filters" action="/search" method="get"></form>

<fieldset form="filters">
  <input form="filters" name="q">
</fieldset>
```

If the input must belong to `#filters`, associate the input itself.

## Rules

- The referenced form must be in the same document.
- The value is the target form's `id`.
- A control has one form owner at a time.
- Normal successful-control and validation rules still apply.
- Do not use this to visually scramble form structure; use it when layout genuinely needs detached actions/controls.
- This is mature HTML and safe for the Firefox 140/Tor baseline.

## Replaces

```text
button outside form -> JS find form -> requestSubmit()/fetch()
```

with explicit browser-owned form association.

## Sources

- MDN: https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/form
- HTML Standard: https://html.spec.whatwg.org/multipage/form-control-infrastructure.html#attr-fae-form
- Can I Use: https://caniuse.com/form-attribute
