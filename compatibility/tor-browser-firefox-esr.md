# Tor Browser / Firefox ESR Baseline

Compatibility snapshot: **2026-09-09**.

Tor Browser stable **15.0.21** is based on **Firefox 140.15.0 ESR**.

Official Tor release:

- https://blog.torproject.org/new-release-tor-browser-15021/

This file records engine-version facts. Tor may apply privacy/security policy changes, so a Firefox-engine fact still requires testing in the exact Tor release and security level.

## Features known to predate Firefox 140

These are available in the Firefox engine baseline, subject to Tor-specific behavior and product testing.

### Semantic HTML / navigation / forms

- real anchors, forms, buttons and standard form submitter semantics are mature platform behavior.
- `<dialog>` — Firefox 98.
- `<search>` — Firefox 118.
- `<details name>` — Firefox 130.
- `autocorrect` — Firefox 136.
- native search/date/range/color/file/select controls, `formaction`, `formmethod`, `formnovalidate`, submitter `name=value`, `fieldset disabled`, `inputmode`, `autocomplete`, `spellcheck`, `aria-current`, `inert`, and ordinary constraint validation all predate this ESR baseline.

### CSS/browser-owned state

- `light-dark()` — Firefox 120.
- `:has()` — Firefox 121.
- Declarative Shadow DOM (`shadowrootmode`) — Firefox 123.
- Popover API, `popovertarget`, `popovertargetaction` — Firefox 125.
- `@starting-style` — Firefox 129.
- `transition-behavior: allow-discrete` — Firefox 129.
- `:open` — Firefox 136.
- `hidden="until-found"` — Firefox 139.
- `:target`, `:focus-visible`, `:focus-within`, `:checked`, `:default`, `:indeterminate`, `:in-range`, `:out-of-range`, `:placeholder-shown`, link states, logical properties, Grid/Flexbox, Subgrid, CSS containment, scroll snap, sticky positioning, CSS counters and normal media queries are older than this ESR baseline.

### Layout/performance/input preferences

- container **size** queries predate Firefox 140 and may be used for component layout after testing.
- `content-visibility: auto` and `contain-intrinsic-size` predate this baseline; remember they do not reduce DOM/data size.
- dynamic viewport units (`dvh` / `svh` / `lvh`) predate this baseline.
- `scrollbar-gutter`, safe-area `env()`, `aspect-ratio`, `object-fit`, `min()` / `max()` / `clamp()`, and input capability media queries predate this baseline.
- `prefers-reduced-motion`, `prefers-color-scheme`, `prefers-contrast`, `forced-colors`, `color-scheme`, and the `scripting` media feature are available before this ESR line.

## Explicitly newer than Firefox 140

Do **not** make these core to Tor Browser 15.0.21:

- `::details-content` — Firefox 143.
- generic `command` / `commandfor` invoker commands — Firefox 144.
- CSS Anchor Positioning enabled by default — Firefox 147.
- `popover="hint"` — Firefox 149.
- customizable-select newer picker styling — newer/partial around Firefox 149.
- media state pseudo-classes (`:playing`, `:paused`, `:buffering`, `:muted`, `:seeking`, `:stalled`, `:volume-locked`) — Firefox 150.
- `field-sizing` — Firefox 152.
- `focusgroup` — Chromium 150-era emerging feature, not Firefox 140 baseline.
- `scroll-target-group`, generated scroll buttons/markers and scroll-state query work — newer/emerging feature family.
- `reading-flow` / `reading-order` — Limited Availability/experimental for the conservative target.
- `anchor-scope` / `position-visibility` — part of the newer Anchor Positioning stack.
- Declarative Partial Updates — Chromium/WICG emerging work.
- cross-document View Transitions — not Firefox 140 ESR baseline.
- media playback-state CSS selectors — Firefox 150, therefore presentation enhancement only for newer browsers.

## Features whose syntax exists but must be treated carefully

### Native lazy loading with JavaScript disabled

Do **not** count `loading="lazy"` as a Tor/Safest bandwidth guarantee. Browser lazy-loading behavior has anti-tracking constraints, and MDN notes that deferred loading is tied to scripting being enabled. A page must remain correct if resources load eagerly.

See `primitives/native-lazy-loading-caveat.md`.

### `spellcheck`

Support is old, but privacy is the important boundary: browser configurations may send editable content to a third-party spellchecking service. Sensitive/private fields should explicitly consider `spellcheck="false"`.

### `autocapitalize`

Treat as a harmless input-method hint, not a guaranteed cross-browser behavior. MDN still marks it Limited Availability across the whole browser ecosystem.

### CSS `resize`

Treat arbitrary-element resizing as optional ergonomics; MDN marks the feature Limited Availability across the complete browser landscape.

### `text-wrap` values

Line-wrapping enhancements are presentation only. Do not make content accessibility depend on `balance`, `pretty` or other newer wrapping values.

## Tor-first rules

For a Tor-first / JavaScript-disabled product:

1. test the exact Tor Browser stable release;
2. test the intended security level, including Safest/JS-disabled if that is the contract;
3. never add a JavaScript polyfill and still call the path zero-JS;
4. keep links/forms as complete task paths;
5. make newer platform features progressive enhancement;
6. do not equate current Firefox/MDN Baseline with Firefox ESR;
7. keep native input/gesture behavior intact unless a narrowly-scoped rule intentionally changes it;
8. do not assume browser convenience features such as spellchecking/lazy loading have the same privacy/performance behavior in every configuration.

## Exact Mozilla release references

- `<search>` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/118
- `light-dark()` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/120
- `:has()` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/121
- Declarative Shadow DOM — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/123
- Popover / `popovertargetaction` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/125
- `@starting-style` / `transition-behavior` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/129
- `<details name>` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/130
- `:open` and `autocorrect` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/136
- `hidden="until-found"` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/139
- `::details-content` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/143
- `command` / `commandfor` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/144
- Anchor Positioning — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/147
- `popover="hint"` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/149
- media state pseudo-classes — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/150
- `field-sizing` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/152
