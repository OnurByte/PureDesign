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
compatibility  > pattern convenience
principles     > clever CSS trick
semantics/a11y > visual similarity
```

## Product contract

PureDesign means:

- zero client-side JavaScript for core behavior;
- semantic HTML first;
- browser-owned ephemeral interaction, focus, scroll, layout, form, media and preference state where the platform exposes it;
- URL/server-owned durable application state;
- CSS renders state instead of pretending to be a programming language;
- unsupported new CSS may remove polish, never access to a task;
- server pagination/data limits remain necessary even when CSS can skip off-screen rendering.

## Before writing JavaScript, check the platform owner

### Resize / layout measurement

Before `ResizeObserver`, resize listeners or `getBoundingClientRect()` used only for presentation, check:

- `container-size-queries.md`
- `dynamic-viewport-units.md`
- `safe-area-env.md`
- `aspect-ratio-and-object-fit.md`
- `css-math-responsive-sizing.md`
- `position-sticky.md`
- `scroll-offsets.md`
- `scrollbar-gutter.md`

Use JavaScript only when measurements change actual data/application behavior rather than CSS presentation.

### Scrolling / visibility

Before `scroll` listeners or `IntersectionObserver`, check:

- `position-sticky.md`
- `content-visibility.md`
- `scroll-snap.md`
- `scroll-offsets.md`
- `scroll-state-container-queries.md` (newer enhancement)
- `scroll-target-group.md` (newer enhancement)
- `position-visibility.md` (newer enhancement)

Do not overclaim these. `content-visibility` does not reduce response bytes or DOM node count.

### Native form controls

Before building a custom widget, check whether the task is already a real:

- `<select>`
- checkbox/radio
- date/time input
- range slider
- color picker
- file picker
- `<progress>`
- `<meter>`

Use `accent-color`, `::file-selector-button`, native state pseudo-classes and newer customizable-select styling before replacing semantics solely for branding.

### Mobile input and unknown text direction

Before UA/device/language sniffing, check:

- `inputmode`
- `enterkeyhint`
- `autocomplete` tokens
- `hover` / `pointer` media features
- `dir="auto"`
- `<bdi>`
- `dirname` form submission

### User preferences

Before `matchMedia()` or preference-detection JavaScript used only to alter presentation, check:

- `prefers-color-scheme`
- `prefers-reduced-motion`
- `prefers-contrast`
- `forced-colors`
- `color-scheme`
- `light-dark()`

Respect the user's preference. Do not use `forced-color-adjust: none` or similar overrides broadly to preserve branding.

### Media and files

Before adding a client player/uploader/downloader/source-switcher, check:

- native `<video>/<audio controls>`
- `<track>` for WebVTT captions/subtitles
- `<input type="file">` + multipart form
- optional file `capture` hint, with normal file input retained as fallback
- normal `<a>` download navigation
- `<picture>` / `srcset` / `sizes`

Advanced streaming, chunking, local previews or bespoke media UX may still require another client, but the semantic HTTP/native baseline should remain complete.

## Compatibility discipline

Do not treat an MDN **Baseline 2026** badge as proof of Tor support. Tor Browser 15.0.21 uses Firefox 140.15 ESR.

Examples:

- container **size** queries landed in Firefox 110: inside the Firefox 140 engine baseline.
- `field-sizing` is Baseline 2026 but Firefox only added it in 152: not Tor 140 core.
- `command/commandfor` landed in Firefox 144: not Tor 140 core.
- typed `attr()` for arbitrary CSS properties landed in Firefox 155: not Tor 140 core.
- CSS Anchor Positioning is newer than Firefox 140: enhancement only.
- Popover-specific `popovertargetaction` landed with Firefox 125 Popover support: available in the Firefox 140 engine baseline.

Always compare the exact landing version against the target ESR.

## Native lazy-loading trap

Do **not** assume `loading="lazy"` saves network traffic when scripting is disabled.

Browsers intentionally disable lazy request deferral without scripting as an anti-tracking measure. A Tor/Safest-style no-JS design must budget as if lazy resources can be requested eagerly.

## Performance discipline

Before writing JS measurement/observer code, check relevant primitives such as:

- `content-visibility`
- container size queries
- `field-sizing`
- scroll-state container queries
- Anchor Positioning
- `position-visibility`
- `interpolate-size`
- `scrollbar-gutter`

But do not turn browser-layout features into fake data virtualization. Large datasets still need server limits/pagination.

## Experimental discipline

These are research/progressive features, not excuses to delete stable fallbacks:

- CSS `@scope`
- container style queries
- typed `attr()` in arbitrary properties
- CSS `if()`
- native masonry / Grid Lanes
- Declarative Partial Updates
- `focusgroup`
- `interestfor`

## Do not

- introduce hidden-checkbox hacks when a semantic primitive exists;
- require hydration;
- add JavaScript polyfills and still call the result zero-JS;
- use experimental CSS as the only path to functionality;
- assume current Chrome/Firefox support implies Tor Browser support;
- copy a source project's framework layer when only its browser primitive matters;
- use positive `tabindex` or DOM duplication to repair visual ordering;
- use UA/device sniffing where browser input/layout primitives answer the actual question;
- apply gesture-altering rules such as `overscroll-behavior: none` globally without a specific reason;
- replace native controls solely because their styling is less uniform;
- treat CSS-presentational state as authorization/security state;
- override user motion/contrast/forced-color preferences just to preserve visual branding.
