# `position-visibility`

**Role:** Progressive enhancement for anchor-positioned UI. Newer than the Tor/Firefox 140 ESR baseline.

`position-visibility` lets the browser hide an anchor-positioned element when its anchor is no longer meaningfully visible or when the positioned element would overflow.

```css
.help-bubble {
    position: fixed;
    position-anchor: --help-button;
    position-area: block-start;
    position-visibility: anchors-visible;
}
```

Useful values include:

- `anchors-visible` — hide when the associated anchor is fully hidden
- `anchors-valid` — hide when no valid anchor can be resolved
- `no-overflow` — hide when the positioned element starts overflowing its containing area/viewport
- `always`

## Replaces

A class of overlay bookkeeping based on:

```text
IntersectionObserver
getBoundingClientRect()
scroll/resize listeners
 -> if anchor is gone/offscreen, hide tooltip/menu
```

The layout engine can make this decision directly.

## Prefer repositioning before hiding

For interactive menus and important controls, try to keep the overlay usable with `position-try-fallbacks` / `@position-try` before hiding it.

Conditional hiding is best for contextual content that becomes meaningless without its anchor, such as hints or nonessential callouts.

## Compatibility

MDN marks `position-visibility` as Baseline 2026 across current browsers, but CSS Anchor Positioning itself is newer than Firefox 140 ESR. Treat it as enhancement-only for Tor Browser 15.

## Sources

- MDN: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/position-visibility
- MDN anchor fallback/hiding guide: https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Anchor_positioning/Try_options_hiding
