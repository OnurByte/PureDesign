# PureDesign

**Modern application-like web UI with zero client-side JavaScript.**

PureDesign is an AI-friendly, atomic knowledge base for building interfaces with semantic HTML, CSS, browser-owned state, URLs, native forms and server-rendered responses.

**Every implementation topic lives in its own file.** This README is only the map. AI agents should start with [`AGENTS.md`](AGENTS.md), then read only the files relevant to the task.

## Core model

```text
Ephemeral interaction state -> browser-native HTML state
Form state                  -> native form controls
Navigation state            -> URL
Scroll/layout state         -> browser CSS/layout engine
Durable application state   -> server
Visual state                -> CSS
Client-side JS              -> 0
```

---

# Principles

- [`principles/state-ownership.md`](principles/state-ownership.md) — decide where each kind of state belongs.
- [`principles/semantic-html-first.md`](principles/semantic-html-first.md) — semantic browser primitives before fake widgets.
- [`principles/progressive-enhancement.md`](principles/progressive-enhancement.md) — unsupported new CSS may remove polish, never the task.
- [`principles/server-authoritative-state.md`](principles/server-authoritative-state.md) — durable app state stays in URLs/forms/server responses.
- [`principles/accessibility-and-input.md`](principles/accessibility-and-input.md) — keyboard, touch, hover, focus and assistive-tech rules.
- [`principles/legacy-css-hacks.md`](principles/legacy-css-hacks.md) — where checkbox/radio hacks stop being appropriate.

---

# Stable / conservative primitives

- [`primitives/details.md`](primitives/details.md) — native disclosure and grouped accordions.
- [`primitives/popover.md`](primitives/popover.md) — browser-owned floating panel state.
- [`primitives/popovertargetaction.md`](primitives/popovertargetaction.md) — declarative show/hide/toggle Popover controls.
- [`primitives/dialog.md`](primitives/dialog.md) — native dialog/modal semantics.
- [`primitives/has.md`](primitives/has.md) — propagate descendant state visually without class-toggling JS.
- [`primitives/open-pseudo-class.md`](primitives/open-pseudo-class.md) — style browser-owned open state with `:open`.
- [`primitives/focus-states.md`](primitives/focus-states.md) — `:focus-visible` / `:focus-within`.
- [`primitives/interaction-pseudo-classes.md`](primitives/interaction-pseudo-classes.md) — `:hover` / `:active` feedback.
- [`primitives/input-capability-media-features.md`](primitives/input-capability-media-features.md) — `hover` / `pointer` capability queries instead of device sniffing.
- [`primitives/form-selection-state.md`](primitives/form-selection-state.md) — real `:checked` radio/checkbox state.
- [`primitives/native-validation.md`](primitives/native-validation.md) — native constraints and `:user-invalid` / `:user-valid`.
- [`primitives/target.md`](primitives/target.md) — URL-fragment state via `:target`.
- [`primitives/hidden-until-found.md`](primitives/hidden-until-found.md) — collapsed content that remains Find-in-Page/fragment discoverable.
- [`primitives/inert.md`](primitives/inert.md) — declaratively disable an entire subtree.
- [`primitives/multi-action-forms.md`](primitives/multi-action-forms.md) — `formaction`, `formmethod`, `formtarget`, external submitters.
- [`primitives/datalist.md`](primitives/datalist.md) — native suggestions with known a11y limits.
- [`primitives/color-scheme.md`](primitives/color-scheme.md) — native-control/browser color-scheme integration.
- [`primitives/light-dark.md`](primitives/light-dark.md) — system-following light/dark values without JS detection.
- [`primitives/scripting-media-feature.md`](primitives/scripting-media-feature.md) — CSS detection of script availability in mixed apps.
- [`primitives/scroll-snap.md`](primitives/scroll-snap.md) — browser-owned scroll physics/snapping.
- [`primitives/content-visibility.md`](primitives/content-visibility.md) — skip off-screen layout/paint while keeping semantic DOM.
- [`primitives/scrollbar-gutter.md`](primitives/scrollbar-gutter.md) — prevent scrollbar-driven layout shifts.
- [`primitives/overscroll-behavior.md`](primitives/overscroll-behavior.md) — control nested scroll chaining without wheel/touch handlers.
- [`primitives/declarative-shadow-dom.md`](primitives/declarative-shadow-dom.md) — server-rendered Shadow DOM without `attachShadow()` JS.
- [`primitives/starting-style-and-discrete-transitions.md`](primitives/starting-style-and-discrete-transitions.md) — entry/exit motion without timer JS.
- [`primitives/interpolate-size.md`](primitives/interpolate-size.md) — intrinsic-size animation without measuring heights in JS.

---

# Newer / progressive primitives

- [`primitives/command-and-commandfor.md`](primitives/command-and-commandfor.md) — declarative standardized invoker commands.
- [`primitives/dialog-closedby.md`](primitives/dialog-closedby.md) — declarative dialog dismissal/light-dismiss policy.
- [`primitives/field-sizing-content.md`](primitives/field-sizing-content.md) — native autosizing text inputs/textarea.
- [`primitives/anchor-positioning.md`](primitives/anchor-positioning.md) — browser-native floating UI placement/fallbacks.
- [`primitives/anchor-scope.md`](primitives/anchor-scope.md) — isolate anchor names inside repeated server-rendered components.
- [`primitives/position-visibility.md`](primitives/position-visibility.md) — hide anchored UI when its anchor/placement stops making sense.
- [`primitives/customizable-select.md`](primitives/customizable-select.md) — richer native `<select>` styling.
- [`primitives/focusgroup.md`](primitives/focusgroup.md) — emerging browser-owned roving focus/arrow navigation.
- [`primitives/interestfor-and-hint-popover.md`](primitives/interestfor-and-hint-popover.md) — emerging interest state for hints/hovercards.
- [`primitives/scroll-target-group.md`](primitives/scroll-target-group.md) — emerging CSS-native scrollspy/current-target state.
- [`primitives/scroll-state-container-queries.md`](primitives/scroll-state-container-queries.md) — query stuck/snapped/scrollable state without scroll JS.
- [`primitives/scroll-buttons-and-markers.md`](primitives/scroll-buttons-and-markers.md) — browser-generated carousel controls.
- [`primitives/reading-flow.md`](primitives/reading-flow.md) — emerging visual/sequential-navigation order alignment.
- [`primitives/view-transitions.md`](primitives/view-transitions.md) — MPA navigation polish without SPA routing.
- [`primitives/scroll-driven-animations.md`](primitives/scroll-driven-animations.md) — scroll-linked decoration, never core behavior.
- [`primitives/text-fit.md`](primitives/text-fit.md) — responsive text fitting without measurement loops.

## Research / watchlist

- [`primitives/declarative-partial-updates.md`](primitives/declarative-partial-updates.md) — emerging `<template for>` server-stream patching without inline patch JS.
- [`primitives/native-tooltip-proposals.md`](primitives/native-tooltip-proposals.md) — future browser-owned/styleable tooltip direction.

---

# Patterns

Read a pattern first for a concrete UI problem, then follow its primitive links.

- [`patterns/accordion.md`](patterns/accordion.md) — semantic disclosure/accordion.
- [`patterns/dropdown-action-menu.md`](patterns/dropdown-action-menu.md) — popover action/dropdown menu.
- [`patterns/responsive-navigation.md`](patterns/responsive-navigation.md) — no-JS responsive navigation.
- [`patterns/declarative-dialog-drawer.md`](patterns/declarative-dialog-drawer.md) — newer native modal side drawer/navigation.
- [`patterns/modal-confirmation.md`](patterns/modal-confirmation.md) — confirmation around a real server form action.
- [`patterns/url-tabs.md`](patterns/url-tabs.md) — fragment/server-backed panels.
- [`patterns/theme-switcher.md`](patterns/theme-switcher.md) — system/local/server-owned theme state.
- [`patterns/micro-interactions.md`](patterns/micro-interactions.md) — app-like hover/active/focus feedback.
- [`patterns/autosizing-textarea.md`](patterns/autosizing-textarea.md) — message composer without autosize JS.
- [`patterns/carousel.md`](patterns/carousel.md) — scroll-snap baseline + optional generated controls.
- [`patterns/bottom-sheet.md`](patterns/bottom-sheet.md) — scrolling/snap model instead of pointer physics JS.
- [`patterns/scrollspy.md`](patterns/scrollspy.md) — anchor baseline + optional native current-section state.
- [`patterns/sticky-header-state.md`](patterns/sticky-header-state.md) — stuck-state styling without scroll listeners.
- [`patterns/long-server-rendered-list.md`](patterns/long-server-rendered-list.md) — server pagination + browser render skipping.
- [`patterns/server-filter-sort-pagination.md`](patterns/server-filter-sort-pagination.md) — URL/server-owned data controls.
- [`patterns/multi-action-form.md`](patterns/multi-action-form.md) — Save/Preview/Publish routing without click JS.
- [`patterns/tooltip-hovercard.md`](patterns/tooltip-hovercard.md) — input-safe tooltip/hovercard direction.
- [`patterns/inactive-workflow-panel.md`](patterns/inactive-workflow-panel.md) — permission/workflow gating with `inert`.
- [`patterns/findable-collapsed-content.md`](patterns/findable-collapsed-content.md) — hidden content that remains searchable.
- [`patterns/selectable-cards.md`](patterns/selectable-cards.md) — semantic radio/checkbox cards via `:has()`.
- [`patterns/validation-feedback.md`](patterns/validation-feedback.md) — user validation state + server authority.
- [`patterns/accessibly-reordered-layout.md`](patterns/accessibly-reordered-layout.md) — responsive visual ordering without DOM-reorder JS.
- [`patterns/script-capability-adaptation.md`](patterns/script-capability-adaptation.md) — mixed-app script/no-script capability presentation.
- [`patterns/server-streaming-future.md`](patterns/server-streaming-future.md) — future zero-JS out-of-order server streaming.

---

# Compatibility

- [`compatibility/tor-browser-firefox-esr.md`](compatibility/tor-browser-firefox-esr.md) — exact Tor Browser 15.0.21 / Firefox 140.15 ESR boundaries.
- [`compatibility/feature-matrix.md`](compatibility/feature-matrix.md) — core / polish / conditional / unsupported matrix.
- [`compatibility/testing.md`](compatibility/testing.md) — semantic baseline, target-browser no-JS and newest-browser enhancement tests.

---

# AI retrieval examples

### Zero-JS file action menu for Tor Browser

```text
patterns/dropdown-action-menu.md
 -> primitives/popover.md
 -> primitives/popovertargetaction.md
 -> compatibility/tor-browser-firefox-esr.md
```

### Long server-rendered message list

```text
patterns/long-server-rendered-list.md
 -> primitives/content-visibility.md
 -> patterns/server-filter-sort-pagination.md
```

### Autosizing chat composer

```text
patterns/autosizing-textarea.md
 -> primitives/field-sizing-content.md
 -> compatibility/feature-matrix.md
```

### New-browser native drawer

```text
patterns/declarative-dialog-drawer.md
 -> primitives/dialog.md
 -> primitives/command-and-commandfor.md
 -> primitives/dialog-closedby.md
 -> compatibility/tor-browser-firefox-esr.md
```

The goal is **selective retrieval**, not loading the whole repository.

## License

No license has been selected yet.
