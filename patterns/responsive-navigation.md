# Responsive Navigation

## Conservative baseline

A disclosure can provide a semantic mobile navigation toggle without JavaScript:

```html
<details class="site-nav">
  <summary>Menu</summary>
  <nav>
    <a href="/">Home</a>
    <a href="/files">Files</a>
    <a href="/settings">Settings</a>
  </nav>
</details>
```

Desktop CSS can present the navigation persistently when appropriate.

## Newer direction

On browsers with declarative dialog invoker commands, a navigation overlay may instead compose:

- [`<dialog>`](../primitives/dialog.md)
- `command="show-modal"` / `commandfor`

## Rule

Choose semantics based on the actual design. Do not reach for a hidden checkbox solely because it is easy to style with `:checked`.

## Research source

- https://github.com/picocss/pico/discussions/343
