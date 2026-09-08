# Declarative Shadow DOM

**Role:** create a Shadow DOM boundary directly in server-rendered HTML without `attachShadow()` JavaScript.

```html
<example-menu>
  <template shadowrootmode="open">
    <style>
      :host { display: inline-block; }
    </style>
    <slot></slot>
  </template>
</example-menu>
```

## Why it matters

Server-rendered components can gain style/composition isolation without requiring a client runtime merely to construct the shadow root.

## Boundary

Do not use Shadow DOM everywhere. It changes styling, composition, form and accessibility boundaries. Use it only where isolation provides concrete value.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/template
- https://gist.github.com/YieldRay/3d965bf568332a25c38f8c00fb79285e
