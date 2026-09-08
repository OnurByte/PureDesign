# `:has()`

**Role:** derive parent/ancestor visual state from descendant state without JavaScript class toggling.

Focused field:

```css
.field:has(input:focus-visible) {
  border-color: var(--accent);
}
```

Selected card:

```css
.plan:has(input:checked) {
  border-color: var(--accent);
  background: var(--selected-bg);
}
```

Invalid group:

```css
.field:has(input:user-invalid) {
  border-color: var(--danger);
}
```

## State boundary

`:has()` does not create state. It observes state owned by HTML/browser controls and lets CSS propagate its visual consequence upward.

Use it instead of scripts that merely add `.active`, `.focused`, `.selected` or `.invalid` classes.

## Source

- https://developer.mozilla.org/en-US/docs/Web/CSS/:has
