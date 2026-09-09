# PureDesign

**Modern application-like web UI with zero client-side JavaScript.**

PureDesign is an AI-friendly, atomic knowledge base for building interfaces with semantic HTML, CSS, browser-owned state, URLs, native forms, native media and server-rendered responses.

**Every implementation topic lives in its own file.** This README is only the map. AI agents should start with [`AGENTS.md`](AGENTS.md), then retrieve only the files relevant to the task.

## Core model

```text
Ephemeral interaction state -> browser-native HTML state
Form/input state            -> native controls and constraints
Navigation state            -> real URLs, links and forms
Scroll/layout state         -> browser CSS/layout engine
Media/device affordances    -> browser and operating system
User preferences            -> CSS media features / UA settings
Durable application state   -> server
Visual state                -> CSS
Client-side JS              -> 0
```

---

# Principles

- [`principles/state-ownership.md`](principles/state-ownership.md) — decide whether state belongs to the browser, form, URL, server or CSS.
- [`principles/semantic-html-first.md`](principles/semantic-html-first.md) — use semantic platform primitives before fake widgets.
- [`principles/progressive-enhancement.md`](principles/progressive-enhancement.md) — unsupported new CSS may remove polish, never access to the task.
- [`principles/server-authoritative-state.md`](principles/server-authoritative-state.md) — durable application state remains URL/form/server state.
- [`principles/accessibility-and-input.md`](principles/accessibility-and-input.md) — keyboard, touch, hover, focus and assistive-tech rules.
- [`principles/legacy-css-hacks.md`](principles/legacy-css-hacks.md) — checkbox/radio state-machine history and where those hacks stop being appropriate.

---

# Stable / conservative primitives

## Navigation and location state

- [`primitives/anchor-navigation.md`](primitives/anchor-navigation.md) — preserve real link navigation, new-tab, bookmark, history and copy-link semantics.
- [`primitives/aria-current.md`](primitives/aria-current.md) — expose server-known current page/step/location without client route matching.
- [`primitives/link-and-visited-state.md`](primitives/link-and-visited-state.md) — native link/history presentation plus `:visited` privacy boundaries.
- [`primitives/target.md`](primitives/target.md) — URL fragment state via `:target`.
- [`primitives/scroll-offsets.md`](primitives/scroll-offsets.md) — `scroll-margin` / `scroll-padding` instead of sticky-header offset scripts.
- [`primitives/scroll-behavior.md`](primitives/scroll-behavior.md) — optional native smooth fragment scrolling.
- [`primitives/download-links.md`](primitives/download-links.md) — ordinary browser downloads instead of `fetch -> Blob -> objectURL` glue.
- [`primitives/search-input-and-landmark.md`](primitives/search-input-and-landmark.md) — `<search>`, `role="search"` and `<input type="search">` for server search.

## Browser interaction state

- [`primitives/details.md`](primitives/details.md) — `<details>`, `<summary>` and grouped `<details name>` disclosure state.
- [`primitives/popover.md`](primitives/popover.md) — browser-owned floating panel state.
- [`primitives/popovertargetaction.md`](primitives/popovertargetaction.md) — declarative `show` / `hide` / `toggle` Popover actions.
- [`primitives/dialog.md`](primitives/dialog.md) — native dialog/modal semantics.
- [`primitives/dialog-form-method.md`](primitives/dialog-form-method.md) — close dialogs through `method="dialog"` / `formmethod="dialog"`.
- [`primitives/modal-and-backdrop-state.md`](primitives/modal-and-backdrop-state.md) — `:modal` and `::backdrop` instead of duplicated overlay state.
- [`primitives/open-pseudo-class.md`](primitives/open-pseudo-class.md) — style browser-owned open state using `:open`.
- [`primitives/has.md`](primitives/has.md) — derive parent/ancestor presentation from descendant state.
- [`primitives/focus-states.md`](primitives/focus-states.md) — `:focus-visible` / `:focus-within`.
- [`primitives/interaction-pseudo-classes.md`](primitives/interaction-pseudo-classes.md) — `:hover` / `:active` feedback.
- [`primitives/empty-pseudo-class.md`](primitives/empty-pseudo-class.md) — derive noncritical empty-container presentation from DOM structure.
- [`primitives/hidden-until-found.md`](primitives/hidden-until-found.md) — collapsed content that remains Find-in-Page/fragment discoverable.
- [`primitives/inert.md`](primitives/inert.md) — declaratively disable an entire interaction subtree.

## Forms and submitter semantics

- [`primitives/form-selection-state.md`](primitives/form-selection-state.md) — semantic `:checked` radio/checkbox state.
- [`primitives/default-and-indeterminate-state.md`](primitives/default-and-indeterminate-state.md) — browser-owned `:default` / `:indeterminate` states.
- [`primitives/native-select.md`](primitives/native-select.md) — real `<select>` before custom dropdown reimplementation.
- [`primitives/native-validation.md`](primitives/native-validation.md) — native constraints plus `:user-invalid` / `:user-valid`.
- [`primitives/placeholder-shown.md`](primitives/placeholder-shown.md) — derive placeholder/empty-field presentation without reading values in JS.
- [`primitives/autofill-state.md`](primitives/autofill-state.md) — style browser/password-manager autofill state.
- [`primitives/range-validation-state.md`](primitives/range-validation-state.md) — `:in-range` / `:out-of-range` from native constraints.
- [`primitives/disabled-readonly-state.md`](primitives/disabled-readonly-state.md) — semantic disabled vs read-only behavior.
- [`primitives/fieldset-disabled.md`](primitives/fieldset-disabled.md) — disable a whole group with one semantic attribute.
- [`primitives/multi-action-forms.md`](primitives/multi-action-forms.md) — `formaction`, `formmethod`, `formtarget` and external submitters.
- [`primitives/submitter-name-value.md`](primitives/submitter-name-value.md) — clicked submitter identifies intent in the serialized form payload.
- [`primitives/formnovalidate.md`](primitives/formnovalidate.md) — let one submit action skip browser constraint validation, e.g. Save Draft.
- [`primitives/datalist.md`](primitives/datalist.md) — native suggestions with explicit accessibility limitations.
- [`primitives/date-time-inputs.md`](primitives/date-time-inputs.md) — native date/time pickers and normalized values.
- [`primitives/range-input.md`](primitives/range-input.md) — browser-owned slider interaction.
- [`primitives/color-input.md`](primitives/color-input.md) — browser/OS color picker.
- [`primitives/native-file-upload.md`](primitives/native-file-upload.md) — file picker + multipart upload baseline.
- [`primitives/file-capture-hint.md`](primitives/file-capture-hint.md) — optional mobile capture hint; normal file picker remains fallback.
- [`primitives/file-selector-button.md`](primitives/file-selector-button.md) — style the real file button instead of proxy-clicking a hidden input.
- [`primitives/progress.md`](primitives/progress.md) — semantic task progress.
- [`primitives/meter.md`](primitives/meter.md) — semantic scalar/quota measurement.
- [`primitives/accent-color.md`](primitives/accent-color.md) — brand native checkbox/radio/range/progress controls without rebuilding them.

## Text-entry and mobile input affordances

- [`primitives/inputmode.md`](primitives/inputmode.md) — virtual keyboard hint without device detection.
- [`primitives/enterkeyhint.md`](primitives/enterkeyhint.md) — browser-owned virtual-keyboard action label.
- [`primitives/autocomplete-tokens.md`](primitives/autocomplete-tokens.md) — describe field purpose to autofill/password managers.
- [`primitives/autocorrect.md`](primitives/autocorrect.md) — browser/OS autocorrection; Firefox 136+.
- [`primitives/autocapitalize.md`](primitives/autocapitalize.md) — virtual-keyboard/voice capitalization hint with limited cross-browser availability.
- [`primitives/spellcheck.md`](primitives/spellcheck.md) — browser spellchecking plus the privacy warning for sensitive text.
- [`primitives/input-capability-media-features.md`](primitives/input-capability-media-features.md) — query `hover` / `pointer` capability instead of UA/device sniffing.
- [`primitives/scripting-media-feature.md`](primitives/scripting-media-feature.md) — CSS adaptation to scripting capability in mixed applications.

## Direction and language

- [`primitives/dir-auto.md`](primitives/dir-auto.md) — browser-determined direction for unknown user text.
- [`primitives/bdi.md`](primitives/bdi.md) — isolate unknown-direction inline user content.
- [`primitives/dirname-form-submission.md`](primitives/dirname-form-submission.md) — submit browser-determined text direction with a form value.
- [`primitives/dir-pseudo-class.md`](primitives/dir-pseudo-class.md) — style the browser-computed direction only where flow-relative CSS is not enough.
- [`primitives/lang-pseudo-class.md`](primitives/lang-pseudo-class.md) — language-specific typography from semantic `lang` state.
- [`primitives/logical-properties.md`](primitives/logical-properties.md) — flow-relative spacing/positioning instead of `.rtl` / `.ltr` layout branches.

## User preference and accessibility media

- [`primitives/prefers-color-scheme.md`](primitives/prefers-color-scheme.md) — system/browser theme preference without `matchMedia()` JS.
- [`primitives/prefers-reduced-motion.md`](primitives/prefers-reduced-motion.md) — honor reduced-motion preference in CSS.
- [`primitives/prefers-contrast.md`](primitives/prefers-contrast.md) — adapt to requested contrast.
- [`primitives/forced-colors.md`](primitives/forced-colors.md) — targeted fixes for forced/high-contrast palettes.
- [`primitives/color-scheme.md`](primitives/color-scheme.md) — tell native controls/browser UI which schemes are supported.
- [`primitives/light-dark.md`](primitives/light-dark.md) — system-following light/dark values without theme-detection JS.

## Media and responsive resources

- [`primitives/responsive-images.md`](primitives/responsive-images.md) — `<picture>` / `srcset` / `sizes` instead of source-switching JS.
- [`primitives/native-media-controls.md`](primitives/native-media-controls.md) — browser audio/video player plus WebVTT tracks.
- [`primitives/native-lazy-loading-caveat.md`](primitives/native-lazy-loading-caveat.md) — why native lazy loading cannot be counted as a JS-disabled bandwidth optimization.
- [`primitives/aspect-ratio-and-object-fit.md`](primitives/aspect-ratio-and-object-fit.md) — intrinsic media boxes/cropping without resize measurement JS.

## Layout, scrolling and rendering

- [`primitives/position-sticky.md`](primitives/position-sticky.md) — sticky headers/sidebars without scroll listeners.
- [`primitives/container-size-queries.md`](primitives/container-size-queries.md) — component responsiveness without width-only `ResizeObserver` class state.
- [`primitives/responsive-grid-auto-fit.md`](primitives/responsive-grid-auto-fit.md) — browser-chosen card column count using `auto-fit/minmax`.
- [`primitives/subgrid.md`](primitives/subgrid.md) — align nested/repeated component internals without sibling height measurement.
- [`primitives/css-containment.md`](primitives/css-containment.md) — rendering/layout containment with explicit behavioral caveats.
- [`primitives/content-visibility.md`](primitives/content-visibility.md) — skip off-screen layout/paint while semantic DOM remains present.
- [`primitives/contain-intrinsic-size.md`](primitives/contain-intrinsic-size.md) — reserve/remember size for skipped contained content.
- [`primitives/scroll-snap.md`](primitives/scroll-snap.md) — browser-owned scroll physics and snapping.
- [`primitives/scrollbar-gutter.md`](primitives/scrollbar-gutter.md) — avoid scrollbar-driven layout shift.
- [`primitives/overscroll-behavior.md`](primitives/overscroll-behavior.md) — control nested scroll chaining without wheel/touch handlers.
- [`primitives/dynamic-viewport-units.md`](primitives/dynamic-viewport-units.md) — `dvh` / `svh` / `lvh` instead of `window.innerHeight -> --vh` scripts.
- [`primitives/safe-area-env.md`](primitives/safe-area-env.md) — UA safe-area insets instead of device/notch tables.
- [`primitives/css-math-responsive-sizing.md`](primitives/css-math-responsive-sizing.md) — `min()` / `max()` / `clamp()` instead of responsive size measurement JS.
- [`primitives/text-overflow.md`](primitives/text-overflow.md) — single-line ellipsis without measuring string width.
- [`primitives/text-wrap.md`](primitives/text-wrap.md) — browser-owned balanced/pretty line wrapping without injected `<br>` logic.
- [`primitives/resize.md`](primitives/resize.md) — optional native user-resize handles for simple panels.
- [`primitives/css-counters.md`](primitives/css-counters.md) — presentational numbering derived from document structure.
- [`primitives/declarative-shadow-dom.md`](primitives/declarative-shadow-dom.md) — server-rendered Shadow DOM without `attachShadow()` JS.
- [`primitives/starting-style-and-discrete-transitions.md`](primitives/starting-style-and-discrete-transitions.md) — entry/exit motion without timer JS.
- [`primitives/interpolate-size.md`](primitives/interpolate-size.md) — intrinsic-size animation without measuring heights in JS.

---

# Newer / progressive primitives

These may remove more JavaScript in newer browsers, but must not become the only path for conservative/Tor targets unless compatibility explicitly changes.

- [`primitives/command-and-commandfor.md`](primitives/command-and-commandfor.md) — standardized declarative invoker commands.
- [`primitives/dialog-closedby.md`](primitives/dialog-closedby.md) — declarative dialog dismissal policy.
- [`primitives/field-sizing-content.md`](primitives/field-sizing-content.md) — native autosizing text controls.
- [`primitives/anchor-positioning.md`](primitives/anchor-positioning.md) — browser-native floating UI placement/fallbacks.
- [`primitives/anchor-scope.md`](primitives/anchor-scope.md) — isolate anchor names inside repeated components.
- [`primitives/position-visibility.md`](primitives/position-visibility.md) — hide anchored UI when its anchor/placement stops making sense.
- [`primitives/customizable-select.md`](primitives/customizable-select.md) — richer styling while retaining a real `<select>`.
- [`primitives/container-style-queries.md`](primitives/container-style-queries.md) — descendant presentation from container custom-property state.
- [`primitives/css-scope.md`](primitives/css-scope.md) — subtree-local selectors without runtime scoping classes.
- [`primitives/typed-attr.md`](primitives/typed-attr.md) — feed server-rendered attribute values into CSS properties.
- [`primitives/focusgroup.md`](primitives/focusgroup.md) — emerging browser-owned roving focus/arrow navigation.
- [`primitives/interestfor-and-hint-popover.md`](primitives/interestfor-and-hint-popover.md) — emerging interest state for hints/hovercards.
- [`primitives/scroll-target-group.md`](primitives/scroll-target-group.md) — emerging CSS-native current-section/scrollspy state.
- [`primitives/scroll-state-container-queries.md`](primitives/scroll-state-container-queries.md) — query stuck/snapped/scrollable state without scroll listeners.
- [`primitives/scroll-buttons-and-markers.md`](primitives/scroll-buttons-and-markers.md) — browser-generated carousel controls.
- [`primitives/reading-flow.md`](primitives/reading-flow.md) — emerging visual/sequential-navigation ordering.
- [`primitives/media-state-pseudo-classes.md`](primitives/media-state-pseudo-classes.md) — Firefox 150+ playback state directly in CSS.
- [`primitives/view-transitions.md`](primitives/view-transitions.md) — MPA navigation polish without turning routing into an SPA.
- [`primitives/scroll-driven-animations.md`](primitives/scroll-driven-animations.md) — scroll-linked decoration only.
- [`primitives/text-fit.md`](primitives/text-fit.md) — browser text fitting without measurement loops.

## Research / watchlist

- [`primitives/declarative-partial-updates.md`](primitives/declarative-partial-updates.md) — emerging `<template for>` server-stream patching without inline patch JS.
- [`primitives/native-tooltip-proposals.md`](primitives/native-tooltip-proposals.md) — future browser-owned/styleable tooltip direction.
- [`primitives/css-if.md`](primitives/css-if.md) — experimental value-level CSS conditional logic.
- [`primitives/native-masonry-watchlist.md`](primitives/native-masonry-watchlist.md) — evolving native masonry/Grid Lanes work.
- [`primitives/local-link-watchlist.md`](primitives/local-link-watchlist.md) — future URL-relative link selector; currently unsupported.

---

# Patterns

Patterns compose primitives into concrete UI recipes. Read the pattern first for a task, then follow only its primitive links.

## Navigation and overlays

- [`patterns/current-navigation.md`](patterns/current-navigation.md) — server-rendered active/current navigation without route-matching JS.
- [`patterns/responsive-navigation.md`](patterns/responsive-navigation.md) — no-JS responsive navigation.
- [`patterns/dropdown-action-menu.md`](patterns/dropdown-action-menu.md) — Popover action/dropdown menu.
- [`patterns/declarative-dialog-drawer.md`](patterns/declarative-dialog-drawer.md) — newer native modal side drawer/navigation.
- [`patterns/modal-confirmation.md`](patterns/modal-confirmation.md) — confirmation around a real server action.
- [`patterns/url-tabs.md`](patterns/url-tabs.md) — fragment/server-backed panels.
- [`patterns/sticky-anchor-navigation.md`](patterns/sticky-anchor-navigation.md) — fragment navigation under sticky UI without offset JS.
- [`patterns/scrollspy.md`](patterns/scrollspy.md) — anchor baseline + optional native current-section state.
- [`patterns/tooltip-hovercard.md`](patterns/tooltip-hovercard.md) — conservative tooltip/hovercard path plus newer declarative direction.

## Forms and input

- [`patterns/server-search-form.md`](patterns/server-search-form.md) — GET/search URL state with native search semantics.
- [`patterns/multi-action-form.md`](patterns/multi-action-form.md) — multiple server actions without click routing.
- [`patterns/draft-vs-publish-form.md`](patterns/draft-vs-publish-form.md) — Save Draft vs Publish using submitter state and `formnovalidate`.
- [`patterns/mobile-friendly-form.md`](patterns/mobile-friendly-form.md) — virtual keyboard/autofill hints without device sniffing.
- [`patterns/autosizing-textarea.md`](patterns/autosizing-textarea.md) — composer autosize without JS where supported.
- [`patterns/selectable-cards.md`](patterns/selectable-cards.md) — semantic radio/checkbox cards using `:has()`.
- [`patterns/validation-feedback.md`](patterns/validation-feedback.md) — browser validation feedback + server authority.
- [`patterns/inactive-workflow-panel.md`](patterns/inactive-workflow-panel.md) — permission/workflow gating with `inert`.

## Layout, rendering and responsive UI

- [`patterns/responsive-component.md`](patterns/responsive-component.md) — component adaptation without width-only ResizeObserver state.
- [`patterns/responsive-card-grid.md`](patterns/responsive-card-grid.md) — intrinsic card/file grid without JS column counting.
- [`patterns/aligned-card-internals.md`](patterns/aligned-card-internals.md) — align repeated card rows with Grid/Subgrid instead of max-height JS.
- [`patterns/accessibly-reordered-layout.md`](patterns/accessibly-reordered-layout.md) — visual adaptation without DOM-reorder scripts.
- [`patterns/rtl-safe-layout.md`](patterns/rtl-safe-layout.md) — flow-relative geometry + bidi semantics without RTL branching JS.
- [`patterns/mobile-app-shell.md`](patterns/mobile-app-shell.md) — viewport/safe-area-aware shell without resize/device scripts.
- [`patterns/sticky-header-state.md`](patterns/sticky-header-state.md) — sticky baseline plus newer stuck-state styling.
- [`patterns/long-server-rendered-list.md`](patterns/long-server-rendered-list.md) — server pagination + browser render skipping.
- [`patterns/resizable-panel.md`](patterns/resizable-panel.md) — optional simple user-resizable panel without pointer-drag state machine.
- [`patterns/empty-state.md`](patterns/empty-state.md) — server-owned meaningful empty state + optional DOM-derived presentation.
- [`patterns/balanced-heading.md`](patterns/balanced-heading.md) — heading wrapping without measurement/injected breaks.
- [`patterns/findable-collapsed-content.md`](patterns/findable-collapsed-content.md) — hidden content that remains browser-searchable.

## Scrolling and motion

- [`patterns/carousel.md`](patterns/carousel.md) — scroll-snap baseline + optional generated controls.
- [`patterns/bottom-sheet.md`](patterns/bottom-sheet.md) — scrolling/snap model instead of pointer physics JS.
- [`patterns/micro-interactions.md`](patterns/micro-interactions.md) — hover/active/focus feedback with reduced-motion handling.

## Media, theme and content

- [`patterns/native-media-preview.md`](patterns/native-media-preview.md) — file/storage preview using native browser media controls.
- [`patterns/media-state-styling.md`](patterns/media-state-styling.md) — newer presentation-only media playback state without event-to-class glue.
- [`patterns/theme-switcher.md`](patterns/theme-switcher.md) — system/local/server-owned theme state.
- [`patterns/user-generated-bidi-content.md`](patterns/user-generated-bidi-content.md) — LTR/RTL user content without direction-detection JS.
- [`patterns/script-capability-adaptation.md`](patterns/script-capability-adaptation.md) — mixed app presentation based on scripting capability.

## Server-owned application state

- [`patterns/server-filter-sort-pagination.md`](patterns/server-filter-sort-pagination.md) — URL/server-owned filtering, sorting and pagination.
- [`patterns/server-streaming-future.md`](patterns/server-streaming-future.md) — future zero-JS out-of-order server streaming.

---

# Compatibility

- [`compatibility/tor-browser-firefox-esr.md`](compatibility/tor-browser-firefox-esr.md) — exact Tor Browser 15.0.21 / Firefox 140.15 ESR boundaries.
- [`compatibility/feature-matrix.md`](compatibility/feature-matrix.md) — core / polish / conditional / unsupported classification.
- [`compatibility/testing.md`](compatibility/testing.md) — semantic baseline, target-browser no-JS and newest-browser enhancement test levels.

---

# AI retrieval examples

### Zero-JS file manager

```text
patterns/current-navigation.md
patterns/server-search-form.md
patterns/responsive-card-grid.md
patterns/dropdown-action-menu.md
patterns/multi-action-form.md
patterns/native-media-preview.md
patterns/server-filter-sort-pagination.md
compatibility/feature-matrix.md
```

### Tor Browser action menu

```text
patterns/dropdown-action-menu.md
 -> primitives/popover.md
 -> primitives/popovertargetaction.md
 -> compatibility/tor-browser-firefox-esr.md
```

### Responsive reusable component

```text
patterns/responsive-component.md
 -> primitives/container-size-queries.md
 -> primitives/responsive-grid-auto-fit.md
 -> primitives/subgrid.md
```

### Draft / publish editor

```text
patterns/draft-vs-publish-form.md
 -> primitives/submitter-name-value.md
 -> primitives/formnovalidate.md
 -> primitives/native-validation.md
```

### Long server-rendered list

```text
patterns/long-server-rendered-list.md
 -> primitives/content-visibility.md
 -> primitives/contain-intrinsic-size.md
 -> patterns/server-filter-sort-pagination.md
```

The goal is **selective retrieval**, not loading the whole repository.

## License

No license has been selected yet.
