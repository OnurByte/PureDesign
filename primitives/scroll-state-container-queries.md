# Scroll-state container queries

**Role:** Progressive enhancement / current-browser feature. Do not make core behavior depend on it for Tor Browser 15 / Firefox 140 ESR.

Scroll-state container queries expose browser-owned scroll state to CSS. They can replace JavaScript that watches sticky, snapped, or scrollable state just to toggle presentation classes.

```css
.sticky-shell {
    position: sticky;
    inset-block-start: 0;
    container-type: scroll-state;
}

@container scroll-state(stuck: top) {
    .sticky-ui {
        box-shadow: 0 1px 8px rgb(0 0 0 / .16);
        background: Canvas;
    }
}
```

States under active development/shipping include:

- `stuck` — whether a sticky element is currently stuck to an edge
- `snapped` — whether an item is currently scroll-snapped
- `scrollable` — whether more content exists in a direction
- `scrolled` — recent scroll direction/state in newer work

## Replaces

Typical glue code:

```text
scroll / IntersectionObserver
 -> determine sticky/snapped state
 -> add/remove .is-stuck or .active
 -> CSS
```

becomes:

```text
browser scroll state
 -> @container scroll-state(...)
 -> CSS descendant styling
```

## Important implementation constraint

A scroll-state query styles descendants of the query container. Use a wrapper/inner-element structure when necessary.

## 2026 footgun: layout feedback and flicker

Do **not** aggressively change the dimensions of a sticky element in response to `stuck` state. Changing height/padding can change whether it is considered stuck, which can create a feedback loop, flicker, or jank.

Prefer paint/compositing changes:

- background
- box-shadow
- color
- opacity
- border color

Treat size-changing compact-header effects with suspicion and test them at slow scroll speeds.

## Sources

- MDN guide: https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Conditional_rules/Container_scroll-state_queries
- CSSWG explainer: https://github.com/w3c/csswg-drafts/blob/main/css-conditional-5/scroll_state_explainer.md
- CSSWG flicker issue: https://github.com/w3c/csswg-drafts/issues/13898
- Low-visibility Tailwind discussion: https://github.com/tailwindlabs/tailwindcss/discussions/20128
- Real design-system migration example: https://github.com/facebook/astryx/issues/2344
