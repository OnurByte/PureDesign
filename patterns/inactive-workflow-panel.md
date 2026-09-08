# Inactive Workflow Panel

## Compose

- [`inert`](../primitives/inert.md)
- server-rendered authorization/workflow state

```html
<section inert aria-labelledby="billing-heading">
  <h2 id="billing-heading">Billing</h2>
  <input name="card">
  <button>Pay</button>
</section>
```

The server should decide whether the panel is active and render/remove `inert` accordingly.

## Good uses

- future wizard steps
- permission-gated controls shown for context
- read-only workflow snapshots

## Warning

Do not apply `inert` just to achieve a greyed-out visual appearance. It has behavioral and accessibility effects.
