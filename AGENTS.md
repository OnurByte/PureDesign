# AI Instructions for PureDesign

This repository is an atomic knowledge base for building modern interfaces with zero client-side JavaScript.

## How to read this repository

Do **not** load every file blindly.

1. Read `README.md` only as the map.
2. Read the exact file in `patterns/` matching the UI problem.
3. Follow that pattern's links to the smallest relevant set of files in `primitives/`.
4. Read `principles/` only when a state/semantic/accessibility decision is unclear.
5. Read `compatibility/tor-browser-firefox-esr.md` when Tor Browser or Firefox ESR matters.
6. Read `compatibility/feature-matrix.md` before making a newer primitive core functionality.

## Source-of-truth boundaries

- `principles/` defines architectural rules.
- `primitives/` defines **one browser capability per file**.
- `patterns/` composes primitives into concrete UI solutions; it should link rather than duplicate primitive documentation.
- `compatibility/` decides whether a primitive may be core, enhancement-only, conditional, or experimental.
- Research provenance belongs in the exact primitive/pattern file that uses it; do not create giant source catalogs.

If files conflict:

```text
compatibility > pattern convenience
principles    > clever CSS trick
semantics/a11y > visual similarity
```

## Product contract

PureDesign means:

- zero client-side JavaScript for core behavior;
- semantic HTML first;
- browser-owned ephemeral interaction, focus, scroll and layout state where the platform exposes it;
- URL/server-owned durable application state;
- CSS renders state instead of pretending to be a programming language;
- unsupported new CSS may remove polish, never access to a task;
- server pagination/data limits remain necessary even when CSS can skip off-screen rendering.

## Compatibility discipline

Do not treat an MDN **Baseline 2026** badge as proof of Tor support. Tor Browser 15.0.21 uses Firefox 140.15 ESR.

Examples:

- `field-sizing` is Baseline 2026 but Firefox only added it in 152: not Tor 140 core.
- `command/commandfor` landed in Firefox 144: not Tor 140 core.
- CSS Anchor Positioning is newer than Firefox 140: enhancement only.
- Popover-specific `popovertargetaction` landed with Firefox 125 Popover support: available in the Firefox 140 engine baseline.

Always compare the exact landing version against the target ESR.

## Performance discipline

Do not introduce a client runtime just for presentational/rendering work that the browser can own.

Before writing JS measurement/observer code, check relevant primitives such as:

- `content-visibility`
- `field-sizing`
- scroll-state container queries
- Anchor Positioning
- `position-visibility`
- `interpolate-size`
- `scrollbar-gutter`

But do not overclaim them: for example `content-visibility` skips layout/paint, it does not reduce response bytes or DOM node count.

## Do not

- introduce hidden-checkbox hacks when a semantic primitive exists;
- require hydration;
- add JavaScript polyfills and still call the result zero-JS;
- use experimental CSS as the only path to functionality;
- assume current Chrome/Firefox support implies Tor Browser support;
- copy a source project's framework layer when only its browser primitive matters;
- use positive `tabindex` or DOM duplication to repair visual ordering;
- use UA/device sniffing where input-capability media queries answer the actual question;
- apply gesture-altering rules such as `overscroll-behavior: none` globally without a specific reason.
