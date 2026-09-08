# PureDesign

**Modern web UI with zero client-side JavaScript.**

PureDesign is an AI-friendly, atomic knowledge base for building application-like interfaces with semantic HTML, CSS, browser-owned state, URLs, native forms and server-rendered responses.

The repository is intentionally split into small files. **Do not treat this README as the implementation guide.** Use it to locate the exact principle, primitive or pattern you need.

For AI agents, start with [`AGENTS.md`](AGENTS.md).

## Core model

```text
Ephemeral interaction state -> browser-native HTML state
Form state                  -> native form controls
Navigation state            -> URL
Durable application state   -> server
Visual state                -> CSS
Client-side JS              -> 0
```

---

# Principles

Architectural rules that override clever implementation tricks.

- [`principles/state-ownership.md`](principles/state-ownership.md) — decides whether state belongs to the browser, form, URL, server or CSS.
- [`principles/semantic-html-first.md`](principles/semantic-html-first.md) — use the semantic platform primitive instead of fake checkbox/div widgets.
- [`principles/progressive-enhancement.md`](principles/progressive-enhancement.md) — functionality first; new CSS may add polish but may not become the only task path.
- [`principles/server-authoritative-state.md`](principles/server-authoritative-state.md) — sorting, filtering, CRUD, auth and other durable state remain HTTP/server concerns.
- [`principles/accessibility-and-input.md`](principles/accessibility-and-input.md) — keyboard, touch, focus, hover and accessibility rules for zero-JS UI.

---

# Browser primitives

Each file documents one browser capability, its state boundary, compatibility role and sources.

## Stable / immediately useful primitives

- [`primitives/details.md`](primitives/details.md) — `<details>`, `<summary>` and grouped `<details name>` accordions.
- [`primitives/popover.md`](primitives/popover.md) — declarative floating menus/panels and `:popover-open`.
- [`primitives/dialog.md`](primitives/dialog.md) — `<dialog>` semantics and the difference between the mature element and newer invoker commands.
- [`primitives/has.md`](primitives/has.md) — `:has()` as visual state propagation instead of JavaScript class toggling.
- [`primitives/native-validation.md`](primitives/native-validation.md) — native constraints, `:user-invalid` and `:user-valid`.
- [`primitives/target.md`](primitives/target.md) — URL-fragment state exposed through `:target`.
- [`primitives/hidden-until-found.md`](primitives/hidden-until-found.md) — collapsed content that remains discoverable through Find in Page and fragments.
- [`primitives/inert.md`](primitives/inert.md) — disable an entire subtree declaratively.
- [`primitives/datalist.md`](primitives/datalist.md) — simple native autocomplete suggestions and its accessibility limits.
- [`primitives/declarative-shadow-dom.md`](primitives/declarative-shadow-dom.md) — server-rendered Shadow DOM without `attachShadow()` JavaScript.
- [`primitives/multi-action-forms.md`](primitives/multi-action-forms.md) — `formaction`, `formmethod`, `formtarget` and external form submitters.
- [`primitives/scroll-snap.md`](primitives/scroll-snap.md) — browser scrolling physics and snapping for carousels/bottom-sheet-like interactions.
- [`primitives/starting-style-and-discrete-transitions.md`](primitives/starting-style-and-discrete-transitions.md) — JS-free entry/exit transition primitives.

## Progressive / newer primitives

- [`primitives/anchor-positioning.md`](primitives/anchor-positioning.md) — browser-native floating-element positioning and fallback direction.
- [`primitives/customizable-select.md`](primitives/customizable-select.md) — richer styling while retaining a real `<select>`.
- [`primitives/focusgroup.md`](primitives/focusgroup.md) — emerging declarative roving focus and arrow-key navigation.
- [`primitives/interestfor-and-hint-popover.md`](primitives/interestfor-and-hint-popover.md) — emerging pointer/keyboard/touch interest state for hints and hovercards.
- [`primitives/scroll-target-group.md`](primitives/scroll-target-group.md) — emerging CSS-native current-section tracking / scrollspy state.
- [`primitives/scroll-buttons-and-markers.md`](primitives/scroll-buttons-and-markers.md) — browser-generated carousel buttons and markers.
- [`primitives/view-transitions.md`](primitives/view-transitions.md) — MPA navigation polish without converting routing to an SPA.
- [`primitives/scroll-driven-animations.md`](primitives/scroll-driven-animations.md) — scroll/view timeline decoration; never core content behavior.
- [`primitives/text-fit.md`](primitives/text-fit.md) — emerging responsive text fitting without JS measurement loops.

## Research / watchlist primitives

- [`primitives/declarative-partial-updates.md`](primitives/declarative-partial-updates.md) — emerging `<template for>` server-stream patching without inline patch JS.
- [`primitives/native-tooltip-proposals.md`](primitives/native-tooltip-proposals.md) — future native/styleable tooltip direction such as `::tooltip`.

---

# Patterns

Patterns compose primitives into actual UI solutions. Read the pattern first when solving a concrete component problem, then follow its primitive links.

- [`patterns/accordion.md`](patterns/accordion.md) — semantic accordion/disclosure.
- [`patterns/dropdown-action-menu.md`](patterns/dropdown-action-menu.md) — popover-based action/dropdown menu.
- [`patterns/url-tabs.md`](patterns/url-tabs.md) — fragment/server-backed panels and tab-like navigation.
- [`patterns/theme-switcher.md`](patterns/theme-switcher.md) — temporary radio-driven theme state plus persistent server preference.
- [`patterns/carousel.md`](patterns/carousel.md) — scroll-snap baseline with optional native generated controls.
- [`patterns/bottom-sheet.md`](patterns/bottom-sheet.md) — model a bottom sheet as scrolling rather than pointer-physics JavaScript.
- [`patterns/scrollspy.md`](patterns/scrollspy.md) — normal anchors plus optional CSS-native active-section tracking.
- [`patterns/server-filter-sort-pagination.md`](patterns/server-filter-sort-pagination.md) — URL/server-backed filtering, sorting and pagination.
- [`patterns/multi-action-form.md`](patterns/multi-action-form.md) — Save/Publish/Preview-style actions without click routing scripts.
- [`patterns/tooltip-hovercard.md`](patterns/tooltip-hovercard.md) — input-safe tooltip/hovercard direction and conservative fallback.
- [`patterns/inactive-workflow-panel.md`](patterns/inactive-workflow-panel.md) — server-rendered inactive/permission-gated subtree with `inert`.
- [`patterns/findable-collapsed-content.md`](patterns/findable-collapsed-content.md) — collapsed content that remains browser-searchable.
- [`patterns/selectable-cards.md`](patterns/selectable-cards.md) — real checkbox/radio selection styled as cards through `:has()`.
- [`patterns/validation-feedback.md`](patterns/validation-feedback.md) — native user-validation state plus server authority.
- [`patterns/modal-confirmation.md`](patterns/modal-confirmation.md) — dialog semantics around a real server action.
- [`patterns/server-streaming-future.md`](patterns/server-streaming-future.md) — future zero-JS out-of-order server streaming with Declarative Partial Updates.

---

# Compatibility

Read these before making a new platform feature part of core product behavior.

- [`compatibility/tor-browser-firefox-esr.md`](compatibility/tor-browser-firefox-esr.md) — exact Tor Browser 15.0.21 / Firefox 140.15 ESR baseline and newer-than-ESR features.
- [`compatibility/feature-matrix.md`](compatibility/feature-matrix.md) — quick core/polish/conditional/experimental classification.
- [`compatibility/testing.md`](compatibility/testing.md) — semantic HTML, target-browser no-JS and newest-browser enhancement test levels.

---

# How an AI should use PureDesign

For a request such as **“build a zero-JS dropdown menu for Tor Browser”**:

```text
AGENTS.md
  -> patterns/dropdown-action-menu.md
  -> primitives/popover.md
  -> primitives/anchor-positioning.md
  -> compatibility/tor-browser-firefox-esr.md
  -> compatibility/feature-matrix.md
```

For **“make selectable pricing cards”**:

```text
patterns/selectable-cards.md
  -> primitives/has.md
  -> principles/state-ownership.md
```

For **“make an app-like server-rendered file browser”**:

```text
principles/server-authoritative-state.md
patterns/server-filter-sort-pagination.md
patterns/dropdown-action-menu.md
patterns/multi-action-form.md
compatibility/feature-matrix.md
```

The goal is selective retrieval, not reading one giant research document.

## License

No license has been selected yet.
