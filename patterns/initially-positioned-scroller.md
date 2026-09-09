# Initially Positioned Scroller

Use this when the server knows which item is current and a horizontal/vertical scroller should ideally start near that item.

## Baseline

Keep the scroller fully usable from its default position and expose durable current state in markup:

```html
<ul class="tabs">
  <li><a href="?tab=one">One</a></li>
  <li class="is-current"><a href="?tab=two" aria-current="page">Two</a></li>
  <li><a href="?tab=three">Three</a></li>
</ul>
```

```css
.tabs {
  display: flex;
  overflow-x: auto;
  scroll-snap-type: x proximity;
}

.tabs > li {
  scroll-snap-align: center;
}
```

## Progressive enhancement

```css
.tabs > .is-current {
  scroll-initial-target: nearest;
}
```

Supporting browsers may initialize the scroller at the current item. Browsers without the property simply use normal scroll start.

Do not use this instead of URL/server state; it only controls initial presentation.

## Read

- [`../primitives/scroll-initial-target.md`](../primitives/scroll-initial-target.md)
- [`../primitives/scroll-snap.md`](../primitives/scroll-snap.md)
- [`../primitives/aria-current.md`](../primitives/aria-current.md)
