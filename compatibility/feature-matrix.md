# Feature Matrix

Snapshot: **2026-09-08**.

This file answers one question: may a primitive be core behavior for the conservative PureDesign target?

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
| native constraint validation | Yes | client affordance; server still validates |
| Popover API (`auto`/basic) | Yes on Firefox 140 baseline | menus/panels |
| `@starting-style` | Polish | entry transitions |
| `transition-behavior: allow-discrete` | Polish | exit/entry transitions |
| Declarative Shadow DOM | Verify component semantics | server-rendered isolation |
| `hidden="until-found"` | Yes on Firefox 140 baseline | findable collapsed content |
| `inert` | Yes, when semantics fit | inactive subtree |
| scroll snap | Yes | scroll-based interactions |
| `<datalist>` | Conditional | simple suggestions; a11y limitations |
| `command` / `commandfor` | No for Firefox 140 ESR | newer declarative invocation |
| CSS Anchor Positioning | No for Firefox 140 ESR | floating-position enhancement |
| `popover="hint"` / `interestfor` | No for Firefox 140 ESR | emerging tooltip/hovercard |
| customizable select picker styling | No for Firefox 140 ESR | enhancement |
| `scroll-target-group` | No for conservative baseline | native scrollspy enhancement |
| `::scroll-button()` / `::scroll-marker` | No for conservative baseline | carousel controls enhancement |
| `focusgroup` | No for Firefox 140 ESR | emerging keyboard group navigation |
| scroll-driven animations | No | decorative experiment only |
| cross-document View Transitions | No for Firefox 140 ESR | MPA polish elsewhere |
| Declarative Partial Updates | No | research/future streaming |
| `text-fit` | No for Firefox 140 ESR | presentation enhancement |
| `::tooltip` proposal | No | watchlist only |

## Meaning of labels

**Yes** — may participate in core functionality after product-specific testing.

**Polish** — may improve motion/presentation; losing it cannot remove a task.

**Conditional** — technology exists but UX/accessibility constraints decide whether it is appropriate.

**No** — keep a baseline path that does not depend on it.
