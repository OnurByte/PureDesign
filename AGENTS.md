# AI Instructions for PureDesign

PureDesign is an atomic knowledge base for building modern interfaces that look like they should need JavaScript while using **zero client-side JavaScript**.

## Non-negotiable rule

```text
client-side JavaScript = 0
```

Do not add:

- `<script>`;
- JavaScript modules;
- inline event handlers such as `onclick`;
- hydration;
- client runtimes;
- JavaScript polyfills;
- event-listener glue;
- DOM state machines;
- JavaScript used only as an "optional enhancement" inside a PureDesign implementation.

A backend may use any language/runtime. The restriction is JavaScript executed in the browser.

If the requested interaction cannot be built from semantic HTML, CSS, browser-owned state, native controls, real URLs/forms, and server-rendered responses, report the limitation instead of adding JavaScript.

## How to read this repository

Do **not** load every file blindly.

1. Read `README.md` as the human/AI map.
2. Read the exact file in `patterns/` matching the UI problem.
3. Follow that pattern's links to the smallest relevant set in `primitives/`.
4. Read `principles/` only when state ownership, semantics or accessibility is unclear.
5. Read `compatibility/tor-browser-firefox-esr.md` whenever Tor Browser / Firefox ESR matters.
6. Read `compatibility/feature-matrix.md` before making a newer primitive essential.

## Source-of-truth boundaries

- `principles/` — architecture rules.
- `primitives/` — **one browser/platform capability per file**.
- `patterns/` — concrete compositions; link to primitive files instead of duplicating them.
- `compatibility/` — baseline vs polish vs conditional vs unsupported/experimental.
- Research provenance belongs in the exact primitive/pattern file that uses it.

If files conflict:

```text
zero-client-JS contract > implementation convenience
compatibility           > pattern convenience
principles              > clever CSS trick
semantics/a11y          > visual similarity
```

## Product contract

PureDesign means:

- no client-side JavaScript;
- no hydration;
- no browser-side runtime;
- semantic HTML first;
- browser-owned ephemeral interaction/focus/scroll/layout state where available;
- native controls before reimplemented widgets;
- real URLs/links/forms for navigation and submission;
- URL/server-owned durable application state;
- CSS renders browser/server state instead of becoming an unreadable fake application runtime;
- unsupported new features remove polish, not access to the task;
- impossible requests remain explicitly unsupported instead of being solved with JavaScript.

## Required decision flow

There is no "try HTML/CSS first, then write JavaScript" fallback.

The flow is:

```text
requested UI
  -> find semantic/native/browser primitive
  -> compose with HTML/CSS/URL/form/server state
  -> verify compatibility
  -> if impossible under constraints: say unsupported
```

### Navigation and deep links

For route state, navigation, current-page styling, scrolling, and deep links, check:

- `primitives/anchor-navigation.md`
- `primitives/aria-current.md`
- `primitives/target.md`
- `primitives/text-fragments-and-target-text.md`
- `primitives/scroll-offsets.md`
- `primitives/scroll-behavior.md`

The server already knows the current route. Prefer server-rendered `aria-current` over recreating location state in the browser.

Use a real element `id` for durable structural anchors. Text fragments are useful for exact passages, but copied text in a `#:~:text=` URL is not a stable application identifier and may expose the quoted phrase in URL surfaces.

### Forms and actions

For form routing, detached actions, validation, and multiple submit intents, check:

- native form submission
- `primitives/form-owner-attribute.md`
- `primitives/multi-action-forms.md`
- `primitives/submitter-name-value.md`
- `primitives/formnovalidate.md`
- `primitives/fieldset-disabled.md`
- `primitives/native-validation.md`
- `primitives/search-input-and-landmark.md`

A submit button can live outside the visual form and still belong to it through `form="id"`. The clicked successful submit button can choose endpoint/method or serialize its own intent.

### Native controls

Before inventing a custom dropdown/date/color/file/range/progress/player widget, check:

- `native-select.md`
- `date-time-inputs.md`
- `color-input.md`
- `native-file-upload.md`
- `file-selector-button.md`
- `range-input.md`
- `progress.md`
- `meter.md`
- `native-media-controls.md`

A native control may be visually less exotic, but it gives keyboard, touch, accessibility, OS integration, and fallback behavior without browser-side code.

### Component responsiveness and layout

For responsive behavior, element measurement, sibling-aware presentation, and text metrics, check:

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
- progressive `sibling-index-and-count.md`
- progressive `text-box-trim.md`

If the markup/data stays the same and only layout changes, the CSS layout engine should own the problem.

Do not make sibling math or text-box trimming core on Firefox 140/Tor. They are current-browser presentation tools, not conservative-baseline primitives.

### Rendering/performance and scroll stability

For rendering cost and scroll stability, check:

- `content-visibility.md`
- `contain-intrinsic-size.md`
- `css-containment.md`
- `overflow-anchor.md`

Never overclaim these:

```text
content-visibility != data virtualization
containment         != server pagination
render skipping     != fewer DOM nodes / response bytes
scroll anchoring    != layout-shift prevention
```

Reserve intrinsic geometry first. Keep browser scroll anchoring enabled by default; use `overflow-anchor: none` only for a specific bad anchor candidate. Server pagination/data limits still matter.

### Scroll and floating UI

For scrolling, sticky state, menus, popovers, and floating placement, check:

- `position-sticky.md`
- `scroll-snap.md`
- `scrollbar-gutter.md`
- `overscroll-behavior.md`
- `overflow-anchor.md`
- `popover.md`
- progressive `scroll-initial-target.md`
- progressive `anchor-positioning.md`
- progressive `scroll-state-container-queries.md`
- progressive `position-visibility.md`

`scroll-initial-target` is enhancement-only: current/selected application state still belongs to the server/URL/markup.

### Text direction, locale and input method

For RTL, unknown-direction content, and input hints, check:

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

### User preferences and color

For theme, reduced motion, contrast, input capability, and simple foreground derivation, check:

- `prefers-color-scheme.md`
- `prefers-reduced-motion.md`
- `prefers-contrast.md`
- `forced-colors.md`
- `input-capability-media-features.md`
- `scripting-media-feature.md`
- progressive `contrast-color.md`

`contrast-color()` is not an accessibility proof. Keep the palette constrained and the fallback readable.

### CSS computation

For presentation values that appear to require runtime computation, check mature CSS math/custom properties first. For future-facing experiments also read:

- `css-if.md`
- `css-custom-functions.md`
- `typed-attr.md`

Do not move permissions, durable state, business rules, or data fetching into CSS merely because newer CSS can express more logic.

## Compatibility discipline

Do not equate an MDN **Baseline 2026** badge with Tor Browser support.

Conservative reference target in this repository:

```text
Tor Browser 15.0.21
Firefox 140.15 ESR engine baseline
```

Examples:

- `<search>` is Firefox 118 -> predates ESR 140.
- `::target-text` is Firefox 131 -> predates ESR 140; still verify actual Tor product behavior.
- `autocorrect` is Firefox 136 -> predates ESR 140.
- `:open` is Firefox 136 -> predates ESR 140.
- `hidden="until-found"` is Firefox 139 -> predates ESR 140.
- `::details-content` is Firefox 143 -> not Tor 140 core.
- `command/commandfor` is Firefox 144 -> not Tor 140 core.
- `contrast-color()` is Firefox 146 -> not Tor 140 core.
- CSS Anchor Positioning default is Firefox 147 -> not Tor 140 core.
- media state pseudo-classes are Firefox 150 -> not Tor 140 core.
- `field-sizing` is Firefox 152 -> not Tor 140 core.
- `sibling-index()` / `sibling-count()` are Firefox 154 -> not Tor 140 core.
- `text-box-trim` / `text-box-edge` are Firefox 154 -> not Tor 140 core.
- `scroll-initial-target`, CSS `interactivity`, and custom `@function` have no normal Firefox release support in the 2026-09-09 snapshot -> never Tor 140 core.

Always compare the exact landing version against the target ESR and test the actual Tor release.

## State ownership examples

```text
menu open/closed           -> browser Popover/details/dialog state
selected radio             -> native form control
current page               -> URL/server + aria-current
exact quoted passage       -> optional text fragment; structural anchor remains id/URL
search/filter/sort/page     -> URL/server
form action chosen          -> native submitter + server
detached save button       -> form="id" + native submitter
layout column count         -> Grid/container query
sticky position             -> CSS layout engine
scroll reading position     -> browser scroll anchoring where applicable
current sticky styling      -> newer scroll-state query, enhancement only
initial scroller placement  -> optional scroll-initial-target; current item remains server/URL state
user text direction         -> browser bidi algorithm
media playback              -> browser; newer CSS may observe state
application permissions     -> server
```

## Do not

- add any client-side JavaScript;
- add scripts and call them optional enhancement;
- introduce hidden-checkbox hacks when a semantic primitive exists;
- use `<a href="#">` or fake `div role=link` for ordinary navigation;
- require hydration;
- add JavaScript polyfills and still call the result PureDesign;
- make experimental CSS the only path to functionality;
- assume current Chrome/Firefox support implies Tor support;
- copy a source project's framework layer when only its browser primitive matters;
- use positive `tabindex` or DOM duplication to repair visual ordering;
- use UA/device sniffing when capability media queries answer the real question;
- treat `:visited` as application read/unread state;
- treat CSS-generated content as the sole accessible critical status message;
- disable scroll anchoring globally without a concrete product reason;
- treat CSS `interactivity`/HTML `inert` as authorization;
- apply `overscroll-behavior: none`, aggressive containment, or other behavior-changing optimizations globally without a specific reason.
