# Tor Browser / Firefox ESR Baseline

Compatibility snapshot: **2026-09-08**.

Tor Browser **15.0.21** is based on **Firefox 140.15.0 ESR**.

Official Tor release:

- https://blog.torproject.org/new-release-tor-browser-15021/

## Safe baseline facts

The following landed before Firefox 140 and are therefore available in the Firefox engine baseline used by Tor Browser 15.0.21, subject to Tor-specific policy/auditing:

- `:has()` — Firefox 121
- Declarative Shadow DOM (`shadowrootmode`) — Firefox 123
- Popover API — fully supported in Firefox 125
- `@starting-style` — Firefox 129
- `transition-behavior: allow-discrete` — Firefox 129
- grouped `<details name>` — Firefox 130
- `hidden="until-found"` — Firefox 139
- `<dialog>` itself — available since Firefox 98
- `inert`, ordinary forms, `:target`, scroll snap and normal native form controls are mature baseline technologies

## Explicitly newer than Firefox 140

Do not make these core to Tor Browser 15.0.21:

- `command` / `commandfor` invoker commands — Firefox 144
- CSS Anchor Positioning enabled by default — Firefox 147
- `popover="hint"` — Firefox 149
- customizable-select styling in its newer form — still newer/partial around Firefox 149
- `focusgroup` — Chromium 150-era emerging feature
- `scroll-target-group` / CSS generated scroll controls — emerging/newer feature set
- Declarative Partial Updates — Chromium/WICG emerging work
- cross-document View Transitions — not a Firefox 140 ESR baseline

## Tor-specific rule

Never infer Tor support solely from current Firefox stable. Tor stable tracks Firefox ESR and applies privacy/security audits and changes.

For a Tor-first product:

1. test the exact Tor Browser stable release;
2. test with JavaScript disabled / Safest where that is the product contract;
3. avoid JavaScript polyfills;
4. ensure forms/links remain complete task paths;
5. treat newer UI features as progressive enhancement.

## Official Mozilla release references

- `:has()` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/121
- Declarative Shadow DOM — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/123
- Popover — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/125
- `@starting-style` / `transition-behavior` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/129
- `<details name>` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/130
- `hidden="until-found"` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/139
- `command` / `commandfor` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/144
- Anchor Positioning — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/147
- `popover="hint"` — https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/149
