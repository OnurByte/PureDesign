# PureDesign

**Modern application-like web UI with zero client-side JavaScript.**

PureDesign is an AI-oriented knowledge base for building interfaces from semantic HTML, browser-owned state, CSS/layout primitives, native controls, real URLs/forms and server-rendered responses.

This README is **only the map**. Each implementation topic has its own file. AI agents should begin with [`AGENTS.md`](AGENTS.md), open the relevant `patterns/` file, then follow only the primitive/compatibility links needed for the task.

```text
interaction/focus/open state -> browser
form state                   -> native controls
navigation state             -> real URL / link / form
layout/scroll state          -> CSS layout engine
user/device preferences      -> UA / CSS media features
application state            -> server
presentation                 -> CSS
client-side JS               -> 0 for core behavior
```

## Principles

- [`principles/state-ownership.md`](principles/state-ownership.md) — ownership rules for browser/form/URL/server/CSS state.
- [`principles/semantic-html-first.md`](principles/semantic-html-first.md) — semantic primitives before fake widgets.
- [`principles/progressive-enhancement.md`](principles/progressive-enhancement.md) — enhancements may disappear; tasks may not.
- [`principles/server-authoritative-state.md`](principles/server-authoritative-state.md) — durable state remains HTTP/server state.
- [`principles/accessibility-and-input.md`](principles/accessibility-and-input.md) — keyboard/touch/focus/a11y rules.
- [`principles/legacy-css-hacks.md`](principles/legacy-css-hacks.md) — boundaries of checkbox/radio/CSS state-machine hacks.

# Primitives

## Navigation, URL and document location

- [`primitives/anchor-navigation.md`](primitives/anchor-navigation.md) — real `<a href>` navigation semantics.
- [`primitives/aria-current.md`](primitives/aria-current.md) — semantic current page/step/location state.
- [`primitives/link-and-visited-state.md`](primitives/link-and-visited-state.md) — link/history presentation and privacy limits.
- [`primitives/local-link-watchlist.md`](primitives/local-link-watchlist.md) — experimental current-document link selector direction.
- [`primitives/target.md`](primitives/target.md) — fragment state through `:target`.
- [`primitives/text-fragments-and-target-text.md`](primitives/text-fragments-and-target-text.md) — exact-text deep links and browser highlight state.
- [`primitives/search-input-and-landmark.md`](primitives/search-input-and-landmark.md) — `<search>` / search landmark / `<input type="search">`.
- [`primitives/download-links.md`](primitives/download-links.md) — normal browser download navigation.
- [`primitives/scroll-offsets.md`](primitives/scroll-offsets.md) — fragment offsets under sticky UI.
- [`primitives/scroll-behavior.md`](primitives/scroll-behavior.md) — optional native smooth scrolling.

## Disclosure, overlays and interaction state

- [`primitives/details.md`](primitives/details.md) — disclosure and grouped accordions.
- [`primitives/details-content.md`](primitives/details-content.md) — newer `::details-content` styling/animation hook.
- [`primitives/popover.md`](primitives/popover.md) — Popover state/top-layer behavior.
- [`primitives/popovertargetaction.md`](primitives/popovertargetaction.md) — Popover show/hide/toggle actions.
- [`primitives/dialog.md`](primitives/dialog.md) — native dialog semantics.
- [`primitives/dialog-form-method.md`](primitives/dialog-form-method.md) — local dialog close through form semantics.
- [`primitives/dialog-closedby.md`](primitives/dialog-closedby.md) — newer dialog dismissal policy.
- [`primitives/modal-and-backdrop-state.md`](primitives/modal-and-backdrop-state.md) — `:modal` / `::backdrop`.
- [`primitives/command-and-commandfor.md`](primitives/command-and-commandfor.md) — newer declarative invoker commands.
- [`primitives/open-pseudo-class.md`](primitives/open-pseudo-class.md) — `:open` state.
- [`primitives/has.md`](primitives/has.md) — derived ancestor presentation state.
- [`primitives/focus-states.md`](primitives/focus-states.md) — focus-visible/focus-within.
- [`primitives/interaction-pseudo-classes.md`](primitives/interaction-pseudo-classes.md) — hover/active feedback.
- [`primitives/empty-pseudo-class.md`](primitives/empty-pseudo-class.md) — DOM-derived empty presentation.
- [`primitives/hidden-until-found.md`](primitives/hidden-until-found.md) — findable/revealable hidden content.
- [`primitives/inert.md`](primitives/inert.md) — inactive subtree semantics.
- [`primitives/css-interactivity.md`](primitives/css-interactivity.md) — experimental CSS-derived inertness.

## Forms, validation and submitters

- [`primitives/form-selection-state.md`](primitives/form-selection-state.md) — checked radio/checkbox state.
- [`primitives/default-and-indeterminate-state.md`](primitives/default-and-indeterminate-state.md) — default/indeterminate state.
- [`primitives/native-validation.md`](primitives/native-validation.md) — native constraints and user-validity state.
- [`primitives/placeholder-shown.md`](primitives/placeholder-shown.md) — placeholder/empty-field presentation.
- [`primitives/autofill-state.md`](primitives/autofill-state.md) — browser autofill state.
- [`primitives/range-validation-state.md`](primitives/range-validation-state.md) — in-range/out-of-range state.
- [`primitives/disabled-readonly-state.md`](primitives/disabled-readonly-state.md) — disabled vs readonly semantics.
- [`primitives/fieldset-disabled.md`](primitives/fieldset-disabled.md) — disable a form group.
- [`primitives/form-owner-attribute.md`](primitives/form-owner-attribute.md) — associate detached controls/actions with a form.
- [`primitives/multi-action-forms.md`](primitives/multi-action-forms.md) — submitter endpoint/method/target overrides.
- [`primitives/submitter-name-value.md`](primitives/submitter-name-value.md) — clicked button intent in form payload.
- [`primitives/formnovalidate.md`](primitives/formnovalidate.md) — per-submitter browser validation bypass.
- [`primitives/form-reset.md`](primitives/form-reset.md) — native reset-to-initial-state behavior and UX warning.

## Native form controls

- [`primitives/native-select.md`](primitives/native-select.md) — baseline native selection UI.
- [`primitives/customizable-select.md`](primitives/customizable-select.md) — newer richer native select styling.
- [`primitives/datalist.md`](primitives/datalist.md) — native suggestions and a11y limits.
- [`primitives/date-time-inputs.md`](primitives/date-time-inputs.md) — native date/time pickers.
- [`primitives/range-input.md`](primitives/range-input.md) — native slider.
- [`primitives/color-input.md`](primitives/color-input.md) — native color picker.
- [`primitives/native-file-upload.md`](primitives/native-file-upload.md) — native file picker/multipart upload.
- [`primitives/file-selector-button.md`](primitives/file-selector-button.md) — style the real file input button.
- [`primitives/file-capture-hint.md`](primitives/file-capture-hint.md) — optional mobile capture hint.
- [`primitives/progress.md`](primitives/progress.md) — task progress.
- [`primitives/meter.md`](primitives/meter.md) — scalar/quota measurement.
- [`primitives/accent-color.md`](primitives/accent-color.md) — native control accenting.

## Text entry, device and browser affordances

- [`primitives/inputmode.md`](primitives/inputmode.md) — virtual keyboard hint.
- [`primitives/enterkeyhint.md`](primitives/enterkeyhint.md) — virtual keyboard action hint.
- [`primitives/autocomplete-tokens.md`](primitives/autocomplete-tokens.md) — autofill/password-manager semantics.
- [`primitives/autocapitalize.md`](primitives/autocapitalize.md) — capitalization input hint.
- [`primitives/autocorrect.md`](primitives/autocorrect.md) — UA/OS autocorrection.
- [`primitives/spellcheck.md`](primitives/spellcheck.md) — browser spellcheck plus privacy caveat.
- [`primitives/input-capability-media-features.md`](primitives/input-capability-media-features.md) — hover/pointer capability queries.
- [`primitives/scripting-media-feature.md`](primitives/scripting-media-feature.md) — CSS scripting-capability query.

## Language, bidi and flow direction

- [`primitives/dir-auto.md`](primitives/dir-auto.md) — infer unknown text direction.
- [`primitives/bdi.md`](primitives/bdi.md) — isolate unknown-direction inline content.
- [`primitives/dirname-form-submission.md`](primitives/dirname-form-submission.md) — submit detected text direction.
- [`primitives/dir-pseudo-class.md`](primitives/dir-pseudo-class.md) — style computed direction.
- [`primitives/lang-pseudo-class.md`](primitives/lang-pseudo-class.md) — style semantic language.
- [`primitives/logical-properties.md`](primitives/logical-properties.md) — flow-relative geometry.

## Preferences, theme and accessibility modes

- [`primitives/prefers-color-scheme.md`](primitives/prefers-color-scheme.md) — light/dark preference.
- [`primitives/prefers-reduced-motion.md`](primitives/prefers-reduced-motion.md) — reduced motion preference.
- [`primitives/prefers-contrast.md`](primitives/prefers-contrast.md) — contrast preference.
- [`primitives/forced-colors.md`](primitives/forced-colors.md) — forced/high-contrast palettes.
- [`primitives/color-scheme.md`](primitives/color-scheme.md) — native control/browser scheme integration.
- [`primitives/light-dark.md`](primitives/light-dark.md) — scheme-dependent CSS values.
- [`primitives/contrast-color.md`](primitives/contrast-color.md) — newer automatic black/white contrast selection.

## Layout and responsive composition

- [`primitives/position-sticky.md`](primitives/position-sticky.md) — sticky positioning without scroll listeners.
- [`primitives/container-size-queries.md`](primitives/container-size-queries.md) — component-width responsiveness.
- [`primitives/container-style-queries.md`](primitives/container-style-queries.md) — newer container style queries.
- [`primitives/responsive-grid-auto-fit.md`](primitives/responsive-grid-auto-fit.md) — intrinsic responsive Grid columns.
- [`primitives/subgrid.md`](primitives/subgrid.md) — nested track alignment.
- [`primitives/css-math-responsive-sizing.md`](primitives/css-math-responsive-sizing.md) — min/max/clamp sizing.
- [`primitives/sibling-index-and-count.md`](primitives/sibling-index-and-count.md) — newer numeric sibling position/count calculations.
- [`primitives/dynamic-viewport-units.md`](primitives/dynamic-viewport-units.md) — dvh/svh/lvh mobile viewport sizing.
- [`primitives/safe-area-env.md`](primitives/safe-area-env.md) — browser safe-area insets.
- [`primitives/aspect-ratio-and-object-fit.md`](primitives/aspect-ratio-and-object-fit.md) — media box sizing/cropping.
- [`primitives/text-overflow.md`](primitives/text-overflow.md) — native truncation.
- [`primitives/text-wrap.md`](primitives/text-wrap.md) — browser line-wrapping strategies.
- [`primitives/text-fit.md`](primitives/text-fit.md) — newer browser text fitting.
- [`primitives/text-box-trim.md`](primitives/text-box-trim.md) — newer font-metric trimming for optical alignment.
- [`primitives/resize.md`](primitives/resize.md) — optional native resize handles.
- [`primitives/reading-flow.md`](primitives/reading-flow.md) — emerging sequential-navigation ordering.

## Scrolling, rendering and performance

- [`primitives/scroll-snap.md`](primitives/scroll-snap.md) — browser scroll physics/snapping.
- [`primitives/scroll-initial-target.md`](primitives/scroll-initial-target.md) — experimental declarative initial scroller target.
- [`primitives/scrollbar-gutter.md`](primitives/scrollbar-gutter.md) — scrollbar layout stability.
- [`primitives/overscroll-behavior.md`](primitives/overscroll-behavior.md) — scroll chaining behavior.
- [`primitives/overflow-anchor.md`](primitives/overflow-anchor.md) — browser scroll anchoring and selective opt-out.
- [`primitives/css-containment.md`](primitives/css-containment.md) — layout/paint/size containment.
- [`primitives/content-visibility.md`](primitives/content-visibility.md) — off-screen render skipping.
- [`primitives/contain-intrinsic-size.md`](primitives/contain-intrinsic-size.md) — intrinsic placeholder/remembered size.
- [`primitives/scroll-state-container-queries.md`](primitives/scroll-state-container-queries.md) — newer stuck/snapped/scrollable state queries.
- [`primitives/scroll-target-group.md`](primitives/scroll-target-group.md) — newer current-scroll-target state.
- [`primitives/scroll-buttons-and-markers.md`](primitives/scroll-buttons-and-markers.md) — generated carousel controls.
- [`primitives/scroll-driven-animations.md`](primitives/scroll-driven-animations.md) — scroll-linked decorative motion.

## Media and resources

- [`primitives/responsive-images.md`](primitives/responsive-images.md) — picture/srcset/sizes source selection.
- [`primitives/native-media-controls.md`](primitives/native-media-controls.md) — native audio/video controls and tracks.
- [`primitives/media-state-pseudo-classes.md`](primitives/media-state-pseudo-classes.md) — Firefox 150+ playback state in CSS.
- [`primitives/native-lazy-loading-caveat.md`](primitives/native-lazy-loading-caveat.md) — lazy-loading caveat with scripting disabled.

## CSS architecture and transitions

- [`primitives/declarative-shadow-dom.md`](primitives/declarative-shadow-dom.md) — server-rendered Shadow DOM.
- [`primitives/css-scope.md`](primitives/css-scope.md) — newer subtree selector scoping.
- [`primitives/css-counters.md`](primitives/css-counters.md) — structural presentational numbering.
- [`primitives/starting-style-and-discrete-transitions.md`](primitives/starting-style-and-discrete-transitions.md) — declarative entry/exit motion.
- [`primitives/interpolate-size.md`](primitives/interpolate-size.md) — intrinsic-size animation.
- [`primitives/view-transitions.md`](primitives/view-transitions.md) — MPA/navigation visual transitions.

## Floating UI and newer browser-owned state

- [`primitives/anchor-positioning.md`](primitives/anchor-positioning.md) — native floating UI placement.
- [`primitives/anchor-scope.md`](primitives/anchor-scope.md) — repeated-component anchor isolation.
- [`primitives/position-visibility.md`](primitives/position-visibility.md) — anchor/overflow-aware visibility.
- [`primitives/focusgroup.md`](primitives/focusgroup.md) — emerging browser-owned roving focus.
- [`primitives/interestfor-and-hint-popover.md`](primitives/interestfor-and-hint-popover.md) — emerging hint/interest state.

## Research / watchlist

- [`primitives/declarative-partial-updates.md`](primitives/declarative-partial-updates.md) — emerging native server-stream DOM patching.
- [`primitives/native-tooltip-proposals.md`](primitives/native-tooltip-proposals.md) — future styleable/browser-owned tooltips.
- [`primitives/css-if.md`](primitives/css-if.md) — experimental CSS value conditionals.
- [`primitives/css-custom-functions.md`](primitives/css-custom-functions.md) — experimental author-defined CSS value functions.
- [`primitives/typed-attr.md`](primitives/typed-attr.md) — newer typed HTML attribute values in CSS.
- [`primitives/native-masonry-watchlist.md`](primitives/native-masonry-watchlist.md) — evolving native masonry/Grid Lanes.

# Patterns

## Navigation / overlays

- [`patterns/current-navigation.md`](patterns/current-navigation.md) — server-rendered current navigation.
- [`patterns/responsive-navigation.md`](patterns/responsive-navigation.md) — no-JS responsive navigation.
- [`patterns/dropdown-action-menu.md`](patterns/dropdown-action-menu.md) — Popover action menu.
- [`patterns/declarative-dialog-drawer.md`](patterns/declarative-dialog-drawer.md) — newer native dialog drawer.
- [`patterns/modal-confirmation.md`](patterns/modal-confirmation.md) — native dialog + real server action.
- [`patterns/url-tabs.md`](patterns/url-tabs.md) — fragment/server-backed panels.
- [`patterns/sticky-anchor-navigation.md`](patterns/sticky-anchor-navigation.md) — fragment navigation under sticky UI.
- [`patterns/scrollspy.md`](patterns/scrollspy.md) — anchor baseline + progressive native scrollspy.
- [`patterns/citable-text-deep-links.md`](patterns/citable-text-deep-links.md) — exact-passage deep links with ordinary URL fallback.
- [`patterns/tooltip-hovercard.md`](patterns/tooltip-hovercard.md) — conservative + newer native hint direction.

## Forms

- [`patterns/server-search-form.md`](patterns/server-search-form.md) — GET/server-rendered search.
- [`patterns/multi-action-form.md`](patterns/multi-action-form.md) — multiple actions without click routing.
- [`patterns/detached-form-actions.md`](patterns/detached-form-actions.md) — sticky/header/footer actions associated to a distant form.
- [`patterns/draft-vs-publish-form.md`](patterns/draft-vs-publish-form.md) — draft vs publish semantics.
- [`patterns/mobile-friendly-form.md`](patterns/mobile-friendly-form.md) — input-method/autofill hints.
- [`patterns/autosizing-textarea.md`](patterns/autosizing-textarea.md) — progressive native composer autosize.
- [`patterns/selectable-cards.md`](patterns/selectable-cards.md) — semantic radio/checkbox cards.
- [`patterns/validation-feedback.md`](patterns/validation-feedback.md) — browser validation + server authority.
- [`patterns/inactive-workflow-panel.md`](patterns/inactive-workflow-panel.md) — inert workflow/permission state.

## Responsive / layout / performance

- [`patterns/responsive-component.md`](patterns/responsive-component.md) — container-responsive component.
- [`patterns/responsive-card-grid.md`](patterns/responsive-card-grid.md) — intrinsic card/file grid.
- [`patterns/aligned-card-internals.md`](patterns/aligned-card-internals.md) — Subgrid card alignment.
- [`patterns/item-count-aware-layout.md`](patterns/item-count-aware-layout.md) — progressive sibling-index/count presentation.
- [`patterns/accessibly-reordered-layout.md`](patterns/accessibly-reordered-layout.md) — visual order without DOM-reorder JS.
- [`patterns/rtl-safe-layout.md`](patterns/rtl-safe-layout.md) — bidi/logical-property layout.
- [`patterns/mobile-app-shell.md`](patterns/mobile-app-shell.md) — dynamic viewport + safe area shell.
- [`patterns/sticky-header-state.md`](patterns/sticky-header-state.md) — sticky baseline + progressive stuck state.
- [`patterns/long-server-rendered-list.md`](patterns/long-server-rendered-list.md) — server limits + render skipping.
- [`patterns/resizable-panel.md`](patterns/resizable-panel.md) — optional native panel resizing.
- [`patterns/empty-state.md`](patterns/empty-state.md) — server semantic empty state + derived presentation.
- [`patterns/balanced-heading.md`](patterns/balanced-heading.md) — browser text wrapping.
- [`patterns/findable-collapsed-content.md`](patterns/findable-collapsed-content.md) — hidden but browser-searchable content.

## Scroll / motion

- [`patterns/carousel.md`](patterns/carousel.md) — scroll-snap carousel.
- [`patterns/initially-positioned-scroller.md`](patterns/initially-positioned-scroller.md) — server-known current item + progressive initial scroll target.
- [`patterns/stable-scroll-content.md`](patterns/stable-scroll-content.md) — reserved geometry plus browser scroll anchoring.
- [`patterns/bottom-sheet.md`](patterns/bottom-sheet.md) — scrolling/snap bottom-sheet model.
- [`patterns/micro-interactions.md`](patterns/micro-interactions.md) — hover/active/focus motion with reduced-motion handling.

## Media / theme / user content

- [`patterns/native-media-preview.md`](patterns/native-media-preview.md) — native file/media preview.
- [`patterns/media-state-styling.md`](patterns/media-state-styling.md) — progressive media playback-state styling.
- [`patterns/theme-switcher.md`](patterns/theme-switcher.md) — system/local/server theme state.
- [`patterns/automatic-contrast-surfaces.md`](patterns/automatic-contrast-surfaces.md) — server color token + progressive browser-selected foreground.
- [`patterns/user-generated-bidi-content.md`](patterns/user-generated-bidi-content.md) — unknown-direction user content.
- [`patterns/script-capability-adaptation.md`](patterns/script-capability-adaptation.md) — mixed app scripting capability presentation.

## Server-owned state

- [`patterns/server-filter-sort-pagination.md`](patterns/server-filter-sort-pagination.md) — URL/server filtering/sorting/pagination.
- [`patterns/server-streaming-future.md`](patterns/server-streaming-future.md) — future declarative out-of-order server streaming.

# Compatibility

- [`compatibility/tor-browser-firefox-esr.md`](compatibility/tor-browser-firefox-esr.md) — Tor Browser 15.0.21 / Firefox 140.15 ESR boundary.
- [`compatibility/feature-matrix.md`](compatibility/feature-matrix.md) — core/polish/conditional/unsupported classification.
- [`compatibility/testing.md`](compatibility/testing.md) — zero-JS test protocol.

# Suggested AI retrieval paths

```text
file manager
  -> current-navigation
  -> server-search-form
  -> responsive-card-grid
  -> dropdown-action-menu
  -> multi-action-form
  -> native-media-preview
  -> server-filter-sort-pagination

Tor action menu
  -> dropdown-action-menu
  -> popover
  -> popovertargetaction
  -> tor-browser-firefox-esr

long server-rendered list
  -> long-server-rendered-list
  -> stable-scroll-content
  -> overflow-anchor
  -> content-visibility
  -> contain-intrinsic-size
  -> server-filter-sort-pagination

draft/publish editor
  -> draft-vs-publish-form
  -> detached-form-actions
  -> form-owner-attribute
  -> submitter-name-value
  -> formnovalidate
  -> native-validation

citation / evidence link
  -> citable-text-deep-links
  -> text-fragments-and-target-text
  -> target

current item in horizontal scroller
  -> initially-positioned-scroller
  -> aria-current
  -> scroll-snap
  -> scroll-initial-target
```

The goal is **selective retrieval**, not loading the repository wholesale.

## License

PureDesign is licensed under the [0BSD License](LICENSE). You may use, copy, modify, and distribute it for any purpose, including commercial use, without an attribution requirement.