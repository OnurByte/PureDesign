# `inert`

**Role:** declaratively make an entire subtree non-interactive and unfocusable.

```html
<section class="billing-panel" inert>
  <input name="card">
  <button>Pay</button>
</section>
```

Server-rendered example:

```html
<section @if(!$canEdit) inert @endif>
```

```css
[inert] { opacity: .55; }
```

## Good uses

- permission-gated panels
- inactive wizard stages
- read-only snapshots

## Warning

`inert` is stronger than visual dimming. It affects focus, interaction, selection, find-in-page and accessibility exposure. Do not use it merely as a styling hook.

## Source

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes/inert
