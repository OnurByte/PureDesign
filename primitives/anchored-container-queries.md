# Anchored Container Queries

**Role:** style descendants of an anchor-positioned element according to which `position-try-fallbacks` option the browser is currently using, without measuring geometry in JavaScript.

## Representative shape

```html
<button class="trigger">Help</button>

<div class="tooltip">
  <div class="tooltip-surface">
    <span class="tooltip-arrow" aria-hidden="true"></span>
    Helpful text
  </div>
</div>
```

```css
.trigger {
  anchor-name: --help-trigger;
}

.tooltip {
  position: absolute;
  position-anchor: --help-trigger;
  position-area: top;
  position-try-fallbacks: flip-block;
  container-type: anchored;
}

.tooltip-arrow {
  /* points toward an anchor below the tooltip */
  transform: rotate(0deg);
}

@container anchored(fallback: flip-block) {
  .tooltip-arrow {
    /* tooltip moved below the anchor; flip the arrow too */
    transform: rotate(180deg);
  }
}
```

The browser first chooses placement through Anchor Positioning. The anchored query then exposes which fallback is active so descendant presentation can follow that placement.

## Replaces

```text
measure tooltip + viewport
 -> infer whether fallback/flip happened
 -> toggle placement class in JavaScript
 -> reposition arrow/decoration
```

## Descendant rule

As with other container queries, the query styles descendants of the query container, not the query container itself. Put fallback-dependent visual styling on an inner surface/arrow when necessary.

## Scope

Use anchored queries for presentation that follows browser-owned placement:

- tooltip/popover arrow direction;
- gradient direction;
- corner radii appropriate to the active side;
- alignment/padding changes that do not determine whether the UI exists.

Do not use this to make an otherwise unusable overlay suddenly functional. Keep a conventional placement fallback when Anchor Positioning itself is unavailable.

## Compatibility

Snapshot: **2026-09-10**.

- Chromium/Edge: supported from 143 in current compatibility data.
- Firefox: not supported through current 155-era releases in the snapshot.
- Safari: not supported in current releases in the snapshot.
- Tor Browser 15 / Firefox 140 ESR: **not supported**.

Therefore this is progressive enhancement only and must never be required for core behavior on the repository's conservative target.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Anchor_positioning/Anchored_container_queries
- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/container-type
- https://caniuse.com/wf-container-anchor-position-queries
