# Tor Browser / Firefox ESR Baseline

Compatibility snapshot: **2026-09-08**.

Tor Browser **15.0.21** is based on **Firefox 140.15.0 ESR**.

Official Tor release:

- https://blog.torproject.org/new-release-tor-browser-15021/

## Safe baseline facts

The following landed before Firefox 140 and are therefore available in the Firefox engine baseline used by Tor Browser 15.0.21, subject to Tor-specific policy/auditing:

- `light-dark()` — Firefox 120
- `:has()` — Firefox 121
- Declarative Shadow DOM (`shadowrootmode`) — Firefox 123
- Popover API, `popovertarget`, `popovertargetaction` — fully supported in Firefox 125
- `@starting-style` — Firefox 129
- `transition-behavior: allow-discrete` — Firefox 129
- grouped `<details name>` — Firefox 130
- `:open` — Firefox 136
- `hidden="until-found"` — Firefox 139
- `<dialog>` itself — available since Firefox 98
- `inert`, ordinary forms, `:target`, scroll snap, standard input-capability media queries, `color-scheme`, and normal native form controls are mature baseline technologies
- `scripting` media queries and `content-visibility: auto` are mainstream features predating this ESR baseline
- `scrollbar-gutter` is a mainstream 2024-era layout-stability feature predating Firefox 140

## Explicitly newer than Firefox 140

Do not make these core to Tor Browser 15.0.21:

- `command` / `commandfor` invoker commands — Firefox 144
- `::details-content` — Firefox 143 (important: grouped `<details name>` is older, but this styling pseudo-element is newer than ESR 140)
- CSS Anchor Positioning enabled by default — Firefox 147
- `popover="hint"` — Firefox 149
- customizable-select styling in its newer form — newer/partial around Firefox 149
- `field-sizing` — Firefox 152
- `focusgroup` — Chromium 150-era emerging feature
- `scroll-target-group` / CSS generated scroll controls — emerging/newer feature set
- scroll-state container queries — not a Firefox 140 ESR core feature
- `reading-flow` / `reading-order` — experimental / Limited Availability
- `anchor-scope` / `position-visibility` — part of the newer Anchor Positioning stack, not ESR 140 baseline
- Declarative Partial Updates — Chromium/WICG emerging work
- cross-document View Transitions — not a Firefox 140 ESR baseline

## Features that are safe only as polish

Some capabilities do not need a hard yes/no for product behavior because the component must work without them anyway:

- intrinsic-size animation via `interpolate-size`
- `calc-size()` experiments
- advanced entry/exit animation
- scroll-driven animation

If unsupported, the UI should simply become instant/static rather than unusable.

## Tor-specific rule

Never infer Tor support solely from current Firefox stable or from an MDN "Baseline 2026" badge. Tor stable tracks Firefox ESR and applies privacy/security audits and changes.

For a Tor-first product:

1. test the exact Tor Browser stable release;
2. test with JavaScript disabled / Safest where that is the product contract;
3. avoid JavaScript polyfills;
4. ensure forms/links remain complete task paths;
5. treat newer UI features as progressive enhancement;
6. keep native gesture/input behavior intact unless a narrowly-scoped CSS rule intentionally changes it.

## Official Mozilla release references

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
