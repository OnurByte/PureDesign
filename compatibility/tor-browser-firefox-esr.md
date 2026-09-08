# Tor Browser / Firefox ESR Baseline

Compatibility snapshot: **2026-09-08**.

Tor Browser **15.0.21** is based on **Firefox 140.15.0 ESR**.

Official Tor release:

- https://blog.torproject.org/new-release-tor-browser-15021/

## Safe baseline facts

The following landed before Firefox 140 and are therefore available in the Firefox engine baseline used by Tor Browser 15.0.21, subject to Tor-specific policy/auditing and product testing:

- `::file-selector-button` — Firefox 82
- `:autofill` — Firefox 86
- `<dialog>` — Firefox 98
- dynamic viewport units (`svh`, `lvh`, `dvh`, etc.) — Firefox 101
- `:modal` — Firefox 103
- container **size** queries — Firefox 110
- `light-dark()` — Firefox 120
- `:has()` — Firefox 121
- Declarative Shadow DOM (`shadowrootmode`) — Firefox 123
- Popover API, `popovertarget`, `popovertargetaction` — fully supported in Firefox 125
- `@starting-style` — Firefox 129
- `transition-behavior: allow-discrete` — Firefox 129
- grouped `<details name>` — Firefox 130
- `:open` — Firefox 136
- `hidden="until-found"` — Firefox 139

Mature technologies also well inside this baseline include:

- semantic links, buttons and ordinary forms;
- normal `<select>`, checkbox, radio, date/time/range/color/file controls;
- `method="dialog"` behavior within dialogs;
- `<progress>` and `<meter>`;
- `accent-color`;
- native validation and range state;
- `inputmode`, `enterkeyhint`, `autocomplete` tokens;
- `dir="auto"` and `<bdi>`;
- `<picture>`, `srcset`, `sizes`;
- native `<video>/<audio controls>` and `<track>`;
- `position: sticky`;
- `scroll-margin`, `scroll-padding`, scroll snap;
- `aspect-ratio`, `object-fit`;
- `min()`, `max()`, `clamp()`;
- `text-overflow`;
- safe-area `env()` variables;
- `inert`, `:target`, normal focus/input-capability media queries, `color-scheme`;
- `scripting` media queries and `content-visibility: auto`;
- `scrollbar-gutter` and `overscroll-behavior`.

## Explicitly newer than Firefox 140

Do not make these core to Tor Browser 15.0.21:

- `::details-content` — Firefox 143 (grouped `<details name>` itself is older)
- `command` / `commandfor` invoker commands — Firefox 144
- CSS Anchor Positioning enabled by default — Firefox 147
- `popover="hint"` — Firefox 149
- customizable-select styling in its newer form — newer/partial around Firefox 149
- `field-sizing` — Firefox 152
- typed `attr()` in arbitrary CSS properties — Firefox 155
- CSS `@scope` — current-browser/Baseline 2026 feature, not ESR 140 baseline
- container style queries — not an interoperable Firefox 140 baseline feature
- CSS `if()` — Limited Availability / experimental
- native CSS masonry / Grid Lanes — still evolving/early-testing
- `focusgroup` — Chromium 150-era emerging feature
- `scroll-target-group` / CSS generated scroll controls — emerging/newer feature set
- scroll-state container queries — not a Firefox 140 ESR core feature
- `reading-flow` / `reading-order` — experimental / Limited Availability
- `anchor-scope` / `position-visibility` — part of the newer Anchor Positioning stack, not ESR 140 baseline
- Declarative Partial Updates — Chromium/WICG emerging work
- cross-document View Transitions — not a Firefox 140 ESR baseline

## Special no-JS caveat: native lazy loading

Do **not** infer that `loading="lazy"` will save bandwidth when scripting is disabled.

MDN documents that browsers only defer native lazy resource loading when JavaScript is enabled. This is an anti-tracking measure: otherwise a server could infer approximate scroll position from when strategically placed lazy resources are requested.

For a Tor/Safest-style contract, treat `loading="lazy"` as optional progressive metadata, not as a network-budget guarantee.

## Features that are safe only as polish

Some capabilities do not need a hard yes/no for product behavior because the component must work without them anyway:

- intrinsic-size animation via `interpolate-size`;
- advanced entry/exit animation;
- scroll-driven animation;
- newer value-level CSS helpers.

If unsupported, the UI should simply become instant/static rather than unusable.

## Tor-specific rule

Never infer Tor support solely from current Firefox stable or from an MDN "Baseline 2026" badge. Tor stable tracks Firefox ESR and applies privacy/security audits and changes.

For a Tor-first product:

1. test the exact Tor Browser stable release;
2. test with JavaScript disabled / Safest where that is the product contract;
3. avoid JavaScript polyfills;
4. ensure forms/links remain complete task paths;
5. treat newer UI features as progressive enhancement;
6. keep native gesture/input behavior intact unless a narrowly-scoped CSS rule intentionally changes it;
7. do not depend on lazy-loading request deferral when scripting is disabled.

## Official Mozilla release references

- `::file-selector-button` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/82
- `:autofill` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/86
- `<dialog>` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/98
- dynamic viewport units — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/101
- `:modal` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/103
- container size queries — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/110
- `light-dark()` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/120
- `:has()` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/121
- Declarative Shadow DOM — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/123
- Popover / `popovertargetaction` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/125
- `@starting-style` / `transition-behavior` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/129
- `<details name>` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/130
- `:open` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/136
- `hidden="until-found"` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/139
- `::details-content` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/143
- `command` / `commandfor` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/144
- Anchor Positioning — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/147
- `popover="hint"` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/149
- `field-sizing` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/152
- typed `attr()` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/155
