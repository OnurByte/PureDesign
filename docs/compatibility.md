# Compatibility and Progressive Enhancement

PureDesign is intentionally conservative about feature support.

A modern CSS feature is useful only if the product remains usable when that feature is unavailable.

This document uses **2026-09-08** as its compatibility snapshot.

---

## Reference conservative target: Tor Browser stable

As of 2026-09-08, Tor Browser **15.0.21** is based on **Firefox 140.15.0 ESR**.

Official Tor release note:

https://blog.torproject.org/new-release-tor-browser-15021/

This matters because a feature available in current Firefox is not automatically available in current Tor Browser stable.

For a Tor-first application, test against the actual ESR base instead of saying “Firefox supports it.”

---

# Compatibility tiers

## Tier A — core behavior

A feature may be part of core product behavior only when the declared browser baseline actually supports it.

Typical candidates:

- semantic links and forms
- `<details>` / `<summary>`
- real checkbox/radio state
- `:checked`
- `:target`
- `:focus-visible`
- `:focus-within`
- Grid / Flexbox
- custom properties
- standard media queries
- ordinary CSS transitions
- native form constraint validation
- `:has()` when your baseline supports it
- Popover API when your baseline supports it

The rule is stronger than “Can I Use is green.”

Verify the exact target browser/version.

---

## Tier B — polish

These features may improve motion or presentation, but losing them must not remove functionality.

Examples:

- `@starting-style`
- `transition-behavior: allow-discrete`
- intrinsic-size animation helpers
- newer `<details>` animation hooks
- decorative transitions

Correct fallback:

```text
supported   -> smooth component
unsupported -> instant but fully usable component
```

Incorrect fallback:

```text
supported   -> component works
unsupported -> content inaccessible
```

---

## Tier C — experimental / newer enhancement

These are useful research targets, but should not be the sole path for conservative browser matrices.

### CSS Anchor Positioning

Firefox enabled CSS Anchor Positioning by default in **Firefox 147**.

MDN Firefox 147 release notes:

https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/147

Tor Browser 15.0.21 is based on Firefox 140 ESR, so Anchor Positioning cannot be treated as a Tor-stable baseline feature at this snapshot.

Use:

```css
.menu-wrap {
    position: relative;
}

.menu {
    position: absolute;
    inset-block-start: calc(100% + .5rem);
    inset-inline-end: 0;
}
```

as the ordinary fallback, then enhance:

```css
@supports (position-anchor: --trigger) {
    /* anchor-positioning enhancement */
}
```

### Declarative dialog commands

Firefox added support for the `<button>` `command` and `commandfor` attributes in **Firefox 144**.

MDN Firefox 144 release notes:

https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/144

Therefore a Tor Browser based on Firefox 140 ESR must not require `command="show-modal"` / `commandfor` for a core task.

The dialog itself is older; the warning here is specifically about newer declarative invocation behavior.

### Scroll-driven animations

Even in Firefox **155**, scroll-driven animations are listed as an experimental feature disabled by default in release builds.

MDN Firefox 155 release notes:

https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/155

Do not make content visibility, navigation, or task completion depend on:

```css
animation-timeline: view();
```

or related scroll/view timeline primitives for conservative Firefox/Tor targets.

Use them only as nonessential decoration.

### Cross-document View Transitions

A same-origin multi-page application can opt into cross-document transitions with CSS such as:

```css
@view-transition {
    navigation: auto;
}
```

No JavaScript is required for the basic MPA transition model.

MDN overview:

https://developer.mozilla.org/en-US/docs/Web/API/View_Transition_API/Using

However, Firefox 147 release notes explicitly described support for SPA view-transition types while **not supporting cross-document view-transition types** at that point.

https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/147

For Tor/Firefox-ESR-first products, cross-document transitions are therefore enhancement-only until the actual target version supports them.

---

# Progressive-enhancement template

A useful CSS structure is:

```css
/* Baseline: fully functional */
.component {
    /* simple layout */
}

/* Better interaction styling */
@media (prefers-reduced-motion: no-preference) {
    .component {
        transition: opacity 120ms ease;
    }
}

/* Newer optional capability */
@supports (some-new-property: some-value) {
    .component {
        /* enhancement only */
    }
}
```

Do not reverse the hierarchy by putting the only usable layout inside `@supports`.

---

# Tor/Safest design rules

For an application whose contract is “works in Tor Browser with JavaScript disabled”:

1. **Never require client hydration.** The HTML response must already represent the page.
2. **Do not use JavaScript polyfills.** A polyfilled no-JS feature is no longer a zero-client-JS feature.
3. **Keep authoritative state on the server.** Forms and links must remain complete interaction paths.
4. **Test keyboard behavior.** CSS-only is not automatically accessible.
5. **Prefer browser semantics over hidden-input hacks.** Native disclosure/popover/dialog controls expose more meaningful behavior.
6. **Make motion optional.** Respect `prefers-reduced-motion` and assume animation features can disappear.
7. **Avoid external runtime dependencies.** A page should not need third-party JS/CDN behavior to become interactive.
8. **Use exact browser versions in compatibility decisions.** “Firefox supports X” is too vague for ESR/Tor targets.

---

# Feature decision matrix

| Feature | Core in conservative target? | Recommended use |
|---|---:|---|
| `<details>` / `<summary>` | Yes | Core disclosure/accordion behavior |
| Native links/forms | Yes | Core navigation and mutation |
| `:checked` | Yes | Real selection/toggle state |
| `:target` | Yes | Simple URL-fragment state |
| `:focus-visible` | Yes | Keyboard focus feedback |
| `:focus-within` | Yes | Group focus styling |
| `:has()` | Verify exact baseline | Parent/derived visual state |
| Popover API | Verify exact baseline | Native dropdown/action menu |
| `@starting-style` | Enhancement | Entry/exit polish |
| Discrete transitions | Enhancement | Overlay/disclosure polish |
| Declarative Shadow DOM | Verify baseline + semantics | Optional server-rendered isolation |
| `command` / `commandfor` | No for Firefox 140 ESR | Future dialog/command enhancement |
| CSS Anchor Positioning | No for Firefox 140 ESR | Floating-position enhancement |
| Scroll-driven animations | No | Decorative experiment only |
| Cross-document View Transitions | No for this Tor snapshot | MPA navigation polish elsewhere |

---

# Testing strategy

For each component, test three levels:

## Level 1 — semantic HTML only

Disable author CSS if practical.

Can the user still understand and complete the task?

## Level 2 — target browser + CSS + JavaScript disabled

This is the real PureDesign contract.

Check:

- keyboard navigation
- focus visibility
- form submission
- back/forward behavior
- refresh behavior
- open/close semantics
- long-content layout
- reduced motion

## Level 3 — newest browser

Verify optional enhancements such as:

- Anchor Positioning
- advanced transitions
- newer dialog commands
- view transitions

The Level 3 result may look better, but it must not unlock functionality unavailable at Level 2.

---

# Bottom line

PureDesign should treat the web platform as a ladder:

```text
semantic HTML
      |
      v
stable CSS
      |
      v
native browser state
      |
      v
server-rendered application state
      |
      v
new CSS/HTML enhancements
```

Never invert that ladder by making a new visual feature the foundation of the product.
