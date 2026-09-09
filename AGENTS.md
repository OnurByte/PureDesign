# AI Instructions for PureDesign

PureDesign is an atomic knowledge base for building modern interfaces with **zero client-side JavaScript for core behavior**.

## How to read this repository

Do **not** load every file blindly.

1. Read `README.md` only as the map.
2. Read the exact file in `patterns/` matching the UI problem.
3. Follow that pattern's links to the smallest relevant set in `primitives/`.
4. Read `principles/` only when state ownership, semantics or accessibility is unclear.
5. Read `compatibility/tor-browser-firefox-esr.md` whenever Tor Browser / Firefox ESR matters.
6. Read `compatibility/feature-matrix.md` before making a newer primitive core functionality.

## Source-of-truth boundaries

- `principles/` — architecture rules.
- `primitives/` — **one browser/platform capability per file**.
- `patterns/` — concrete compositions; link to primitive files instead of duplicating them.
- `compatibility/` — core vs polish vs conditional vs unsupported/experimental.
- Research provenance belongs in the exact primitive/pattern file that uses it.

If files conflict:

```text
compatibility > pattern convenience
principles    > clever CSS trick
semantics/a11y > visual similarity
```

## Product contract

PureDesign means:

- no hydration requirement;
- no client runtime required for core tasks;
- semantic HTML first;
- browser-owned ephemeral interaction/focus/scroll/layout state where available;
- native controls before reimplemented widgets;
- real URLs/links/forms for navigation and submission;
- URL/server-owned durable application state;
- CSS renders browser/server state instead of becoming an unreadable state machine;
- unsupported new features remove polish, not access to the task.

## Decision flow before writing JavaScript

### Navigation

Before route-click or route-active JS, check:

- `primitives/anchor-navigation.md`
- `primitives/aria-current.md`
- `primitives/target.md`
- `primitives/scroll-offsets.md`
- `primitives/scroll-behavior.md`

The server already knows the current route. Prefer server-rendered `aria-current` over `location.pathname -> .active` logic.

### Forms and actions

Before click handlers or request-building code, check:

- native form submission
- `primitives/multi-action-forms.md`
- `primitives/submitter-name-value.md`
- `primitives/formnovalidate.md`
- `primitives/fieldset-disabled.md`
- `primitives/native-validation.md`
- `primitives/search-input-and-landmark.md`

The clicked successful submit button can already choose endpoint/method or serialize its own intent.

### Native controls

Before custom dropdown/date/color/file/range/progress/player widgets, check:

- `native-select.md`
- `date-time-inputs.md`
- `color-input.md`
- `native-file-upload.md`
- `file-selector-button.md`
- `range-input.md`
- `progress.md`
- `meter.md`
- `native-media-controls.md`

A native control may be visually less exotic, but it often gives keyboard, touch, accessibility, OS integration and fallback behavior for free.

### Component responsiveness and layout

Before `resize` listeners, `ResizeObserver`, manual column counts or sibling measurement, check:

- `container-size-queries.md`
- `responsive-grid-auto-fit.md`
- `subgrid.md`
- `aspect-ratio-and-object-fit.md`
- `css-math-responsive-sizing.md`
- `position-sticky.md`
- `logical-properties.md`
- `text-wrap.md`
- `text-overflow.md`
- `dynamic-viewport-units.md`
- `safe-area-env.md`

If the markup/data stays the same and only layout changes, the layout engine should usually own the problem.

### Rendering/performance

Before adding a runtime solely to reduce paint/layout work, check:

- `content-visibility.md`
- `contain-intrinsic-size.md`
- `css-containment.md`

But never overclaim these:

```text
content-visibility != data virtualization
containment         != server pagination
render skipping     != fewer DOM nodes / response bytes
```

Server pagination/data limits still matter.

### Scroll and floating UI

Before scroll listeners, pointer-physics or positioning libraries, check:

- `position-sticky.md`
- `scroll-snap.md`
- `scrollbar-gutter.md`
- `overscroll-behavior.md`
- `popover.md`
- progressive `anchor-positioning.md`
- progressive `scroll-state-container-queries.md`
- progressive `position-visibility.md`

### Text direction, locale and input method

Before RTL branches/device sniffing/text-input helper JS, check:

- `dir-auto.md`
- `bdi.md`
- `dir-pseudo-class.md`
- `lang-pseudo-class.md`
- `logical-properties.md`
- `inputmode.md`
- `enterkeyhint.md`
- `autocomplete-tokens.md`
- `autocapitalize.md`
- `autocorrect.md`
- `spellcheck.md`

For sensitive fields, remember `spellcheck` may involve third-party services in some browser configurations.

### User preferences

Before `matchMedia()` used only to change CSS, check:

- `prefers-color-scheme.md`
- `prefers-reduced-motion.md`
- `prefers-contrast.md`
- `forced-colors.md`
- `input-capability-media-features.md`
- `scripting-media-feature.md`

## Compatibility discipline

Do not equate an MDN **Baseline 2026** badge with Tor Browser support.

Conservative reference target in this repository:

```text
Tor Browser 15.0.21
Firefox 140.15 ESR engine baseline
```

Examples:

- `<search>` is Firefox 118 -> predates ESR 140.
- `autocorrect` is Firefox 136 -> predates ESR 140.
- `:open` is Firefox 136 -> predates ESR 140.
- `hidden="until-found"` is Firefox 139 -> predates ESR 140.
- `command/commandfor` is Firefox 144 -> not Tor 140 core.
- CSS Anchor Positioning default is Firefox 147 -> not Tor 140 core.
- media state pseudo-classes are Firefox 150 -> not Tor 140 core.
- `field-sizing` is Firefox 152 -> not Tor 140 core.

Always compare the exact landing version against the target ESR and then test the actual Tor release.

## State ownership examples

```text
menu open/closed           -> browser Popover/details/dialog state
selected radio             -> native form control
current page               -> URL/server + aria-current
search/filter/sort/page     -> URL/server
form action chosen          -> native submitter + server
layout column count         -> Grid/container query
sticky position             -> CSS layout engine
current sticky styling      -> newer scroll-state query, enhancement only
user text direction         -> browser bidi algorithm
media playback              -> browser; newer CSS may observe state
application permissions     -> server
```

## Do not

- introduce hidden-checkbox hacks when a semantic primitive exists;
- use `<a href="#">` or fake `div role=link` for ordinary navigation;
- require hydration;
- add JavaScript polyfills and still call the result zero-JS;
- make experimental CSS the only path to functionality;
- assume current Chrome/Firefox support implies Tor support;
- copy a source project's framework layer when only its browser primitive matters;
- use positive `tabindex` or DOM duplication to repair visual ordering;
- use UA/device sniffing when capability media queries answer the real question;
- treat `:visited` as application read/unread state;
- treat CSS-generated content as the sole accessible critical status message;
- apply `overscroll-behavior: none`, aggressive containment or other behavior-changing optimizations globally without a specific reason.
