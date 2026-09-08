# `:target`

**Role:** expose URL-fragment navigation state to CSS.

```html
<nav>
  <a href="#general">General</a>
  <a href="#security">Security</a>
</nav>

<section id="general" class="panel">...</section>
<section id="security" class="panel">...</section>
```

```css
.panel { display: none; }
.panel:target { display: block; }
```

## Benefits

- deep links
- refresh persistence
- bookmarks
- browser back/forward
- no state synchronization script

## Boundary

Use fragment state only when URL-fragment semantics make sense. For sorting, filtering, pagination and durable application state, prefer query parameters/server rendering.

## Source

- https://developer.mozilla.org/en-US/docs/Web/CSS/:target
