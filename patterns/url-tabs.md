# URL-Backed Tabs / Panels

## Compose

- [`:target`](../primitives/target.md) for simple fragment-backed panels
- [server-authoritative state](../principles/server-authoritative-state.md) for durable/query-backed tabs

## Simple fragment version

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

## Choose server state when

The active panel changes data loading, permissions, pagination, filtering or other application truth.

## Do not

Force `:target` into a full ARIA tab widget if the resulting keyboard/semantic behavior is wrong. Native URL navigation is valuable only when its semantics fit.
