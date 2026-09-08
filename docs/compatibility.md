# Compatibility and Progressive Enhancement

PureDesign is intentionally conservative about feature support.

A modern HTML/CSS feature is useful only if the product remains usable when that feature is unavailable.

Compatibility snapshot: **2026-09-08**.

---

## Reference conservative target: Tor Browser stable

As of 2026-09-08, Tor Browser **15.0.21** is based on **Firefox 140.15.0 ESR**.

Official Tor release note:
https://blog.torproject.org/new-release-tor-browser-15021/

This matters because current Firefox and current Chromium ship features that are not in Firefox 140 ESR.

For Tor-first software, never use “Firefox supports it” as the compatibility test. Use the exact ESR version shipped by Tor.

---

# Features that are stronger than they first appear in Firefox 140 ESR

## `<details name>` — yes

Firefox 130 added grouped `<details>` behavior, allowing exclusive accordions without JavaScript.

Source:
https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/130

```html
<details name="settings">...</details>
<details name="settings">...</details>
```

This can be core behavior for the Firefox 140 ESR snapshot.

## Popover API (`auto`) — yes

Firefox 125 fully supported the Popover API, including declarative `popovertarget` and `:popover-open`.

Source:
https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/125

```html
<button popovertarget="menu">Menu</button>
<div id="menu" popover>...</div>
```

Therefore basic declarative popovers are available in Firefox 140 ESR.

Important distinction: `popover="hint"` arrived later in Firefox 149, so do not treat the hint stack as part of the Firefox 140 ESR baseline.

Source:
https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/149

## `hidden="until-found"` — yes

Firefox 139 added `hidden=until-found`.

Source:
https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/139

This is especially valuable in dense no-JS pages because hidden content can still be revealed by browser find-in-page or fragment navigation.

Do not destroy the behavior with a blanket reset:

```css
/* bad */
[hidden] {
    display: none !important;
}
```

Prefer:

```css
[hidden]:where(:not([hidden="until-found"])) {
    display: none !important;
}
```

## `inert` — yes

The `inert` attribute has been broadly available across browsers since 2023.

Source:
https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes/inert

It is suitable for server-rendered inactive subtrees, provided the visual state clearly communicates that the content is unavailable.

## Native form routing — yes

`form`, `formaction`, `formmethod`, `formenctype`, and `formtarget` are mature HTML features.

Sources:

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/button
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/form

These can replace a surprising amount of submit-button click routing and are excellent Tier-A tools for server-rendered apps.

---

# Compatibility tiers

## Tier A — core behavior

Use for essential tasks when verified in the declared browser baseline.

For the Firefox 140 ESR reference snapshot, strong candidates include:

- semantic links/buttons/forms
- `<details>` / `<summary>`
- grouped `<details name>`
- basic Popover API / `popovertarget`
- native checkbox/radio/select controls
- `:checked`
- `:target`
- `:focus-visible`
- `:focus-within`
- `:has()`
- native constraint validation
- `:user-valid` / `:user-invalid`
- `hidden="until-found"`
- `inert`
- `form` / `formaction` / `formmethod`
- Grid / Flexbox
- media/container queries supported by the baseline
- CSS custom properties
- ordinary transitions
- CSS Scroll Snap as ordinary scrolling enhancement

The rule is still stronger than “Can I Use is green”: test the real target.

---

## Tier B — polish

These may improve presentation while remaining nonessential:

- `@starting-style`
- `transition-behavior: allow-discrete`
- newer intrinsic-size animation helpers
- newer `<details>` animation hooks
- decorative transitions
- optional CSS Anchor Positioning where a normal positioning fallback exists

Correct fallback:

```text
supported   -> smooth / better positioned
unsupported -> instant / simpler / still usable
```

---

## Tier C — newer or experimental enhancement

Do not make these the only path for a Firefox 140 ESR / Tor-first product.

### `popover="hint"`

Firefox added `hint` popovers in Firefox 149.

For Firefox 140 ESR, use ordinary `auto` popovers for core behavior and treat hint-stack semantics as future enhancement.

### Declarative dialog commands

Firefox added `command` / `commandfor` support in Firefox 144.

Source:
https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/144

Therefore `command="show-modal"` is not a Firefox 140 ESR core primitive.

### `closedby` on `<dialog>`

Firefox added `closedby` in Firefox 141—just beyond the Firefox 140 ESR snapshot.

Source:
https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/141

Do not assume it exists in the Tor reference target.

### CSS Anchor Positioning

Firefox enabled CSS Anchor Positioning by default in Firefox 147.

Source:
https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/147

For Firefox 140 ESR, retain conventional positioning as the baseline.

### Customizable `<select>` / `appearance: base-select`

In Firefox 149 this was still behind preferences and only partial support was present.

Source:
https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/149

Therefore rich customizable-select rendering is enhancement/research only for the reference target.

Plain `<select>` remains the fallback automatically.

### CSS-native scrollspy: `scroll-target-group` + `:target-current`

This can replace IntersectionObserver-based active-section tracking in supporting browsers.

MDN:
https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/scroll-target-group

It is not a Firefox 140 ESR baseline feature. Keep ordinary anchor navigation as the real product.

### CSS carousel generated controls

New CSS Overflow features include:

- `::scroll-button()`
- `::scroll-marker`
- `::scroll-marker-group`
- `:target-current`

MDN guide:
https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Overflow/Carousels

These can generate stateful carousel controls without JavaScript in newer browsers, but the baseline should remain a normal horizontal scroll container + Scroll Snap.

### `focusgroup`

Chromium 150-class browsers introduced declarative arrow-key / roving-focus navigation for composite widgets.

Sources:

- https://developer.chrome.com/blog/new-in-chrome-150
- https://github.com/whatwg/html/issues/11641

This is not available in Firefox 140 ESR and should remain a watchlist feature.

### `interestfor`

Chromium introduced `interestfor` in Chrome 142 for declarative interest behavior such as hover/focus/touch-triggered popovers.

Source:
https://developer.chrome.com/blog/new-in-chrome-142

Not a Firefox 140 ESR core feature.

### Declarative Partial Updates / `<template for>`

The WICG/Chromium work on Declarative Partial Updates supports declarative out-of-order HTML patching in Chromium 150-class implementations, with additional related APIs still evolving.

Sources:

- https://developer.chrome.com/docs/web-platform/declarative-partial-updates
- https://github.com/WICG/declarative-partial-updates

This is highly relevant to future zero-JS server streaming, but not remotely a Tor/Firefox-ESR baseline yet.

### Scroll-driven animations

Even Firefox 155 release notes still described scroll-driven animation support as experimental/behind preferences.

Source:
https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/155

Never make task completion depend on it.

### Cross-document View Transitions

Cross-document MPA transitions can be declarative/CSS-driven, but Firefox support has lagged the Chromium/Safari direction.

MDN overview:
https://developer.mozilla.org/en-US/docs/Web/API/View_Transition_API/Using

For Firefox 140 ESR, treat this as presentation-only future work.

---

# Special case: `<datalist>`

`<datalist>` can provide browser-native suggestions with no JavaScript, but MDN currently marks it Limited Availability and documents accessibility limitations such as poor styling/high-contrast control and announcement problems in some screen-reader/browser combinations.

Source:
https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/datalist

Therefore PureDesign classifies it as:

```text
simple optional suggestion UX -> potentially useful
universal accessible combobox -> no
```

Do not promote it from “useful native tool” to “always correct replacement.”

---

# Feature decision matrix

| Feature | Firefox 140 ESR / Tor snapshot | PureDesign role |
|---|---:|---|
| Native links/forms | Yes | Core |
| `formaction` / `formmethod` / `form` | Yes | Core server interaction |
| `<details>` / `<summary>` | Yes | Core disclosure |
| `<details name>` | Yes (Firefox 130+) | Core accordion |
| `:checked` | Yes | Core selection state |
| `:target` | Yes | Core/simple fragment state |
| `:focus-visible` / `:focus-within` | Yes | Core focus feedback |
| `:has()` | Yes | Core derived visual state |
| Native form validation / `:user-invalid` | Yes | Core feedback, server remains authoritative |
| Popover `auto` / `popovertarget` | Yes (Firefox 125+) | Core overlay primitive |
| `popover="hint"` | No (Firefox 149+) | Future enhancement |
| `hidden="until-found"` | Yes (Firefox 139+) | Core findable/collapsed content |
| `inert` | Yes | Core server-rendered inactive subtree |
| CSS Scroll Snap | Yes | Core/fallback scroll interaction |
| Declarative Shadow DOM | Verify component semantics | Optional isolation |
| `@starting-style` / discrete transitions | Verify exact property support | Polish only |
| Dialog `command` / `commandfor` | No (Firefox 144+) | Future enhancement |
| Dialog `closedby` | No (Firefox 141+) | Future enhancement |
| CSS Anchor Positioning | No (Firefox 147+) | Floating-position enhancement |
| Customizable select | No | Future enhancement |
| `scroll-target-group` | No | Future CSS-native scrollspy |
| `::scroll-button()` / `::scroll-marker` | No | Future carousel controls |
| `focusgroup` | No | Future keyboard navigation |
| `interestfor` | No | Future interest/tooltip state |
| Declarative Partial Updates | No | Future server-streaming architecture |
| Scroll-driven animations | No | Decorative experiment |
| Cross-document View Transitions | No | Navigation polish elsewhere |

---

# Progressive-enhancement template

```css
/* Level 1: fully functional baseline */
.carousel {
    overflow-x: auto;
    scroll-snap-type: x mandatory;
}

/* Level 2: optional interaction polish */
@media (prefers-reduced-motion: no-preference) {
    .carousel {
        scroll-behavior: smooth;
    }
}

/* Level 3: new platform feature */
@supports (scroll-marker-group: after) {
    .carousel {
        scroll-marker-group: after;
    }

    /* generated controls/markers */
}
```

Functionality lives outside `@supports`.

---

# Tor/Safest design rules

For a contract of “works in Tor Browser with JavaScript disabled”:

1. **No hydration dependency.** The HTML response is already the interface.
2. **No JS polyfill dependency.** A polyfilled feature is not zero-client-JS functionality.
3. **Server owns durable state.** Links/forms must represent complete interaction paths.
4. **Browser owns ephemeral state.** Prefer real disclosure/popover/form/focus state.
5. **Use exact ESR versions.** Current Chromium/Firefox feature posts are not your target matrix.
6. **Preserve browser affordances.** Back/forward, open-in-new-tab, Ctrl+F, keyboard navigation, native autocomplete, and form submission are features.
7. **Do not hide accessibility problems under “semantic.”** Test keyboard, zoom, screen readers, high contrast, and long-content behavior.
8. **Make motion optional.** Unsupported animation must never remove content or controls.
9. **Keep experimental controls additive.** CSS-native scrollspy/carousel controls should sit on top of real links/scroll containers.
10. **Treat future platform proposals as architecture signals, not dependencies.** `focusgroup`, `interestfor`, and `<template for>` show where the platform is going; they do not change today's Tor baseline.

---

# Testing strategy

## Level 1 — semantic HTML only

Disable author CSS if practical.

Can the user still understand the document and complete the task?

## Level 2 — target browser + CSS + JavaScript disabled

For Tor-first work, test the actual Tor Browser stable release/Safest mode.

Check:

- keyboard navigation
- focus visibility
- form submission and submitter-specific routes
- back/forward behavior
- refresh behavior
- open/close semantics
- fragment navigation
- Find in Page, especially with `hidden="until-found"`
- long-content layout
- reduced motion
- zoom/high-contrast behavior

## Level 3 — newest browsers

Verify optional enhancements independently:

- Anchor Positioning
- CSS-native scrollspy
- generated carousel controls
- customizable select
- focusgroup
- interestfor
- advanced dialog commands
- view transitions
- Declarative Partial Updates experiments

Level 3 may feel richer. It must not unlock a task that does not exist at Level 2.

---

# Bottom line

PureDesign's ladder is now broader:

```text
semantic HTML
      |
      v
mature browser behavior
      |
      +--> disclosure / popover / forms / find / inert
      |
      v
stable CSS state rendering
      |
      v
URL + HTTP + server-rendered durable state
      |
      v
new native enhancements
      |
      +--> scrollspy / carousel controls / anchor positioning
      |
      v
future declarative platform
         focusgroup / interestfor / template-for
```

Never invert the ladder by making the newest feature the only path to the product.
