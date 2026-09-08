# Feature Matrix

Snapshot: **2026-09-08**.

This file answers one question: may a primitive be core behavior for the conservative PureDesign / Tor Browser 15 (Firefox 140 ESR) target?

| Primitive | Conservative/Tor core? | Use |
|---|---:|---|
| semantic links/forms/buttons | Yes | core navigation/actions |
| `<details>` / `<summary>` | Yes | disclosure |
| `<details name>` | Yes | exclusive accordion |
| real checkbox/radio/select | Yes | selection/form state |
| `:checked` | Yes | visual selection state |
| `:target` | Yes | fragment-backed state |
| `:focus-visible`, `:focus-within` | Yes | focus feedback |
| `:has()` | Yes on Firefox 140 baseline | derived visual state |
| `:open` | Yes on Firefox 140 baseline | native open-state styling |
| native constraint validation | Yes | client affordance; server still validates |
| `color-scheme` | Yes | UA/native-control scheme integration |
| `light-dark()` | Yes on Firefox 140 baseline | system-following theme values |
| input `hover` / `pointer` media features | Yes | input-capability-aware polish |
| `scripting` media feature | Yes | capability-aware mixed-app fallback |
| Popover API (`auto`/basic) | Yes on Firefox 140 baseline | menus/panels |
| `popovertargetaction` | Yes on Firefox 140 baseline | declarative show/hide/toggle |
| `@starting-style` | Polish | entry transitions |
| `transition-behavior: allow-discrete` | Polish | exit/entry transitions |
| `interpolate-size` | Polish / verify | intrinsic-size animation only |
| `scrollbar-gutter` | Yes/polish | avoid scrollbar-driven layout shift |
| Declarative Shadow DOM | Verify component semantics | server-rendered isolation |
| `hidden="until-found"` | Yes on Firefox 140 baseline | findable collapsed content |
| `inert` | Yes, when semantics fit | inactive subtree |
| scroll snap | Yes | scroll-based interactions |
| `content-visibility: auto` | Yes/progressive performance | skip off-screen layout/paint |
| `overscroll-behavior` | Conditional | prevent nested scroll chaining; gesture side effects |
| `<datalist>` | Conditional | simple suggestions; a11y limitations |
| `command` / `commandfor` | No for Firefox 140 ESR | newer declarative invocation |
| `closedby` | No/verify for Firefox 140 ESR | newer declarative dialog dismissal |
| `field-sizing: content` | No for Firefox 140 ESR | autosizing native fields; Firefox 152+ |
| CSS Anchor Positioning | No for Firefox 140 ESR | floating-position enhancement |
| `anchor-scope` | No for Firefox 140 ESR | isolate repeated anchor components |
| `position-visibility` | No for Firefox 140 ESR | anchor-aware overlay hiding |
| `popover="hint"` / `interestfor` | No for Firefox 140 ESR | emerging tooltip/hovercard |
| customizable select picker styling | No for Firefox 140 ESR | enhancement |
| `scroll-target-group` | No for conservative baseline | native scrollspy enhancement |
| scroll-state container queries | No for conservative baseline | stuck/snapped/scrollable CSS state |
| `::scroll-button()` / `::scroll-marker` | No for conservative baseline | carousel controls enhancement |
| `focusgroup` | No for Firefox 140 ESR | emerging keyboard group navigation |
| `reading-flow` / `reading-order` | No | experimental sequential-navigation ordering |
| scroll-driven animations | No | decorative experiment only |
| cross-document View Transitions | No for Firefox 140 ESR | MPA polish elsewhere |
| Declarative Partial Updates | No | research/future streaming |
| `text-fit` | No for Firefox 140 ESR | presentation enhancement |
| `::tooltip` proposal | No | watchlist only |

## Meaning of labels

**Yes** — may participate in core functionality after product-specific testing.

**Polish** — may improve motion/presentation; losing it cannot remove a task.

**Conditional** — technology exists but UX/accessibility/gesture constraints decide whether it is appropriate.

**No** — keep a baseline path that does not depend on it.

## Baseline warning

A feature marked "Baseline 2026" by MDN is baseline for current mainstream browser releases, **not** automatically for Tor Browser's Firefox ESR engine. Always compare the exact Firefox landing version against the ESR base.
