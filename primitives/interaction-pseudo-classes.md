# `:hover`, `:active`, and Instant CSS Feedback

**Role:** local visual feedback without JavaScript event handlers.

```css
.button {
  transition:
    transform 80ms ease,
    background 120ms ease,
    box-shadow 120ms ease;
}

.button:hover {
  background: var(--hover);
}

.button:active {
  transform: scale(.98);
}
```

Cards can use similarly small hover transitions:

```css
.card {
  transition: transform 120ms ease, background 120ms ease;
}

.card:hover {
  transform: translateY(-1px);
}
```

## Rule

Hover is enhancement, not a task path. Touch and keyboard users must not lose information or controls.

A large part of perceived “app feel” comes from immediate feedback and motion, not from JavaScript itself.
