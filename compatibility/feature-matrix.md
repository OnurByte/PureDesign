# Feature Matrix

Snapshot: **2026-09-08**.

This file answers one question: may a primitive be core behavior for the conservative PureDesign / Tor Browser 15 (Firefox 140 ESR) target?

| Primitive | Conservative/Tor core? | Use |
|---|---:|---|
| semantic links/forms/buttons | Yes | core navigation/actions |
| normal download links/server responses | Yes | file download baseline |
| `<details>` / `<summary>` | Yes | disclosure |
| `<details name>` | Yes | exclusive accordion |
| `<dialog>` element | Yes | dialog semantics; opening path still matters |
| `method="dialog"` | Yes/conditional | local dialog close; not a server mutation |
| `:modal` / `::backdrop` | Yes on Firefox 140 baseline | browser-owned modal styling |
| real checkbox/radio/select | Yes | selection/form state |
| `<input type="file">` + multipart form | Yes | upload baseline |
| file `capture` hint | Conditional | optional mobile camera/mic hint; Limited Availability |
| `::file-selector-button` | Yes on Firefox 140 baseline | style native upload button |
| date/time/range/color native inputs | Yes/conditional UX | browser-owned control; test task suitability |
| `<progress>` / `<meter>` | Yes | semantic status/measurement |
| `accent-color` | Yes | lightweight native-control branding |
| `:checked` | Yes | visual selection state |
| `:placeholder-shown` | Yes | empty/placeholder presentation state |
| `:autofill` | Yes on Firefox 140 baseline | browser autofill state |
| `:in-range` / `:out-of-range` | Yes | range-validation presentation |
| `:disabled` / `:read-only` / `<fieldset disabled>` | Yes | semantic inactive/read-only state |
| `:target` | Yes | fragment-backed state |
| `scroll-margin` / `scroll-padding` | Yes | fragment/snap landing offsets |
| `:focus-visible`, `:focus-within` | Yes | focus feedback |
| `:has()` | Yes on Firefox 140 baseline | derived visual state |
| `:open` | Yes on Firefox 140 baseline | native open-state styling |
| native constraint validation | Yes | client affordance; server still validates |
| `inputmode` / `enterkeyhint` | Yes | virtual-keyboard hints |
| `autocomplete` tokens | Yes | browser/password-manager autofill semantics |
| `dir="auto"` / `<bdi>` | Yes | unknown-direction user text |
| `dirname` form submission | Yes | submit browser-determined text direction |
| `<picture>` / `srcset` / `sizes` | Yes | browser-owned responsive image selection |
| native `<video>/<audio controls>` + `<track>` | Yes | baseline media playback/captions |
| `loading="lazy"` | Conditional; **not a no-JS bandwidth guarantee** | deferral disappears when scripting is disabled |
| `color-scheme` | Yes | UA/native-control scheme integration |
| `prefers-color-scheme` | Yes | system/browser theme preference |
| `light-dark()` | Yes on Firefox 140 baseline | system-following theme values |
| `prefers-reduced-motion` | Yes | motion preference; enhancement behavior only |
| `prefers-contrast` | Yes on Firefox 140 baseline | user-requested contrast adaptation |
| `forced-colors` | Yes/conditional | targeted fixes for forced/high-contrast palettes |
| input `hover` / `pointer` media features | Yes | input-capability-aware polish |
| `scripting` media feature | Yes | capability-aware mixed-app fallback |
| Popover API (`auto`/basic) | Yes on Firefox 140 baseline | menus/panels |
| `popovertargetaction` | Yes on Firefox 140 baseline | declarative show/hide/toggle |
| `position: sticky` | Yes | sticky UI without scroll JS |
| container **size** queries | Yes on Firefox 140 baseline | component responsiveness without ResizeObserver |
| dynamic viewport units (`dvh`/`svh`/`lvh`) | Yes on Firefox 140 baseline | mobile viewport sizing |
| safe-area `env()` | Yes | device/system-safe layout |
| `aspect-ratio` / `object-fit` | Yes | media sizing/cropping |
| CSS `min()` / `max()` / `clamp()` | Yes | bounded responsive sizing |
| `text-overflow: ellipsis` | Yes | single-line visual truncation |
| `@starting-style` | Polish | entry transitions |
| `transition-behavior: allow-discrete` | Polish | exit/entry transitions |
| `interpolate-size` | Polish / verify | intrinsic-size animation only |
| `scrollbar-gutter` | Yes/polish | avoid scrollbar-driven layout shift |
| Declarative Shadow DOM | Verify component semantics | server-rendered isolation |
| `hidden="until-found"` | Yes on Firefox 140 baseline | findable collapsed content |
| `inert` | Yes, when semantics fit | inactive subtree |
| scroll snap | Yes | scroll-based interactions |
| `content-visibility: auto` | Yes/progressive performance | skip off-screen layout/paint; not data virtualization |
| `overscroll-behavior` | Conditional | prevent nested scroll chaining; gesture side effects |
| `<datalist>` | Conditional | simple suggestions; a11y limitations |
| `command` / `commandfor` | No for Firefox 140 ESR | newer declarative invocation |
| `closedby` | No/verify for Firefox 140 ESR | newer declarative dialog dismissal |
| `field-sizing: content` | No for Firefox 140 ESR | autosizing native fields; Firefox 152+ |
| CSS Anchor Positioning | No for Firefox 140 ESR | floating-position enhancement |
| `anchor-scope` | No for Firefox 140 ESR | isolate repeated anchor components |
| `position-visibility` | No for Firefox 140 ESR | anchor-aware overlay hiding |
| `popover="hint"` / `interestfor` | No for Firefox 140 ESR | emerging tooltip/hovercard |
| customizable select picker styling | No for Firefox 140 ESR | enhancement; normal `<select>` is baseline |
| container **style** queries | No for conservative baseline | CSS custom-property state composition |
| CSS `@scope` | No for Firefox 140 ESR | current-browser selector scoping |
| typed `attr()` in arbitrary properties | No for Firefox 140 ESR | current-browser attribute-driven CSS; Firefox 155+ |
| CSS `if()` | No | experimental / Limited Availability |
| native CSS masonry / Grid Lanes | No | evolving early-testing syntax/spec |
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

**Conditional** — technology exists but UX/accessibility/gesture/privacy constraints decide whether it is appropriate.

**No** — keep a baseline path that does not depend on it.

## Baseline warning

A feature marked "Baseline 2026" by MDN is baseline for current mainstream browser releases, **not** automatically for Tor Browser's Firefox ESR engine. Always compare the exact Firefox landing version against the ESR base.

## No-JS loading warning

Native `loading="lazy"` is a special case: browsers intentionally do not defer lazy resource loading when scripting is disabled because request timing could otherwise become a scroll-position tracking channel. Do not count it as a bandwidth-saving guarantee for a Tor/Safest-style no-JS contract.
