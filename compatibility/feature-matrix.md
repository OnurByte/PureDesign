# Feature Matrix

Snapshot: **2026-09-10**.

Conservative reference target: **Tor Browser 15.0.21 / Firefox 140.15 ESR**.

This file answers one question: may a primitive participate in core behavior for that conservative target?

| Primitive | Conservative/Tor core? | Use |
|---|---:|---|
| semantic links/forms/buttons | Yes | core navigation/actions |
| real `<a href>` navigation | Yes | URLs, history, new-tab/bookmark/copy semantics |
| `aria-current` | Yes | server-known current page/step/location |
| `<search>` | Yes on Firefox 140 baseline | search landmark; Firefox 118+ |
| `<input type="search">` | Yes | native search field/form submission |
| `:link` / `:visited` | Yes, presentation only | browser-private link history styling |
| `:local-link` | No | currently unsupported watchlist |
| Text Fragments / `::target-text` | Firefox 140 engine: Yes; verify actual Tor product | exact-passage deep links/highlighting; `::target-text` FF131+; URL privacy caveat |
| `<details>` / `<summary>` | Yes | disclosure |
| `<details name>` | Yes | exclusive accordion |
| `::details-content` | No for Firefox 140 ESR | disclosure-content styling/animation hook; FF143+ |
| Popover API basic/auto | Yes on Firefox 140 baseline | menus/panels |
| `popovertargetaction` | Yes on Firefox 140 baseline | show/hide/toggle Popover |
| `<dialog>` | Yes | dialog semantics |
| `method="dialog"` / `formmethod="dialog"` | Yes | local dialog close/result |
| `:modal` / `::backdrop` | Yes/verify product styling | modal presentation state |
| `:open` | Yes on Firefox 140 baseline | native open-state styling |
| `:has()` | Yes on Firefox 140 baseline | derived visual state |
| `:focus-visible` / `:focus-within` | Yes | focus feedback |
| `:empty` | Yes, presentation caveats | DOM-derived empty-container styling |
| `hidden="until-found"` | Yes on Firefox 140 baseline | findable collapsed content |
| `inert` | Yes when semantics fit | inactive subtree |
| CSS `interactivity` | No | experimental CSS inertness; Chromium 135+, no normal Firefox support at snapshot |
| real checkbox/radio/select | Yes | form selection state |
| `:checked` | Yes | visual selection state |
| `:default` / `:indeterminate` | Yes | browser-owned default/indeterminate presentation |
| native constraint validation | Yes | client affordance; server remains authoritative |
| `:user-invalid` / `:user-valid` | Yes/verify exact UX | user validation feedback |
| `:placeholder-shown` | Yes | field presentation state |
| `:autofill` | Yes/verify styling restrictions | browser autofill presentation |
| `:in-range` / `:out-of-range` | Yes | range constraint presentation |
| `disabled` / `readonly` / `fieldset disabled` | Yes | semantic interaction/submission state |
| explicit `form="id"` ownership | Yes | detached controls/action bars associated with one real form |
| `formaction` / `formmethod` / `formtarget` | Yes | native multi-action routing |
| submitter `name=value` | Yes | clicked action intent in form payload |
| `formnovalidate` | Yes | draft/non-validating browser-submit action |
| native `<select>` | Yes | browser-owned picker |
| `<datalist>` | Conditional | simple suggestions; accessibility limitations |
| native date/time inputs | Yes/conditional UX | browser picker; not ideal for every date task |
| `<input type="range">` | Yes | native slider |
| `<input type="color">` | Yes | native color picker |
| native file input + multipart form | Yes | baseline upload |
| `capture` hint | Conditional | mobile capture hint; Limited Availability |
| `::file-selector-button` | Yes | style real file input button |
| `<progress>` / `<meter>` | Yes | progress vs scalar measurement |
| `accent-color` | Yes | native control branding |
| `inputmode` / `enterkeyhint` | Yes/conditional hint | virtual keyboard hints |
| autocomplete tokens | Yes | autofill/password-manager semantics |
| `autocorrect` | Yes on Firefox 140 baseline | browser/OS correction; Firefox 136+ |
| `autocapitalize` | Conditional | Limited Availability input hint |
| `spellcheck` | Yes/conditional privacy | UA spelling UI; sensitive-data caveat |
| `dir="auto"` / `<bdi>` | Yes | bidi user content |
| `:dir()` / `:lang()` | Yes/verify exact styling target | language/direction-derived presentation |
| CSS logical properties | Yes | RTL/writing-mode-safe geometry |
| `prefers-color-scheme` | Yes | user theme preference |
| `prefers-reduced-motion` | Yes | motion adaptation |
| `prefers-contrast` | Yes on Firefox 140 baseline | contrast preference |
| `forced-colors` | Yes/conditional platform | forced-color adaptation |
| `color-scheme` / `light-dark()` | Yes | native/theme color integration |
| `contrast-color()` | No for Firefox 140 ESR | progressive black/white foreground selection; FF146+; still verify real contrast |
| hover/pointer media features | Yes | input capability adaptation |
| `scripting` media feature | Yes | script capability adaptation |
| `position: sticky` | Yes | sticky layout without scroll JS |
| container size queries | Yes on Firefox 140 baseline | component responsiveness |
| Grid `auto-fit` / `minmax()` | Yes | intrinsic responsive column count |
| CSS Subgrid | Yes | repeated-component track alignment |
| CSS logical sizing/positioning | Yes | direction-safe layout |
| `sibling-index()` / `sibling-count()` | No for Firefox 140 ESR | numeric DOM sibling position/count; Firefox 154+ |
| CSS containment | Yes/conditional | layout/paint isolation; behavior-changing |
| `content-visibility: auto` | Yes/progressive performance | skip off-screen layout/paint |
| `contain-intrinsic-size` | Yes/progressive | placeholder/remembered contained size |
| scroll snap | Yes | browser scroll physics |
| `scroll-initial-target` | No | experimental initial snap target; Chromium 133+, no normal Firefox support at snapshot |
| scroll offsets | Yes | fragment visibility under sticky UI |
| `scroll-behavior` | Yes/polish | smooth native navigation |
| `scrollbar-gutter` | Yes/polish | layout stability |
| `overscroll-behavior` | Conditional | nested scroll chaining; gesture effects |
| `overflow-anchor` | Yes on Firefox 140 / conditional cross-browser | selective scroll-anchoring opt-out; keep default anchoring unless needed |
| dynamic viewport units | Yes on Firefox 140 baseline | mobile viewport sizing |
| safe-area `env()` | Yes/conditional device | display-cutout insets |
| `aspect-ratio` / `object-fit` | Yes | media layout/cropping |
| `min()` / `max()` / `clamp()` | Yes | responsive sizing without measurements |
| `text-overflow` | Yes | truncation presentation |
| `text-wrap: balance/pretty` | Polish / verify value | browser line wrapping quality |
| `text-box-trim` / `text-box-edge` | No for Firefox 140 ESR | typography/optical alignment polish; Firefox 154+ |
| CSS counters | Yes, presentation only | document-structural numbering |
| CSS `resize` | Conditional | simple user resizing; Limited Availability |
| Declarative Shadow DOM | Verify component semantics | server-rendered isolation |
| `@starting-style` | Polish | entry transition |
| `transition-behavior: allow-discrete` | Polish | discrete entry/exit transition |
| `interpolate-size` | Polish / verify | intrinsic-size animation only |
| `command` / `commandfor` | No for Firefox 140 ESR | newer declarative invocation; FF144+ |
| `closedby` | No/verify for Firefox 140 ESR | newer dialog dismissal policy |
| CSS Anchor Positioning | No for Firefox 140 ESR | floating UI positioning; FF147+ |
| anchored container queries | No for Firefox 140 ESR | fallback-aware styling for anchor-positioned descendants; Chromium 143+, no Firefox/Safari support at snapshot |
| `anchor-scope` / `position-visibility` | No for Firefox 140 ESR | newer anchor stack |
| `popover="hint"` / `interestfor` | No for Firefox 140 ESR | newer tooltip/hovercard state |
| customizable select styling | No for Firefox 140 ESR | native-picker enhancement |
| `field-sizing: content` | No for Firefox 140 ESR | autosizing fields; FF152+ |
| `scroll-target-group` | No | native scrollspy enhancement |
| scroll-state container queries | No for conservative baseline | stuck/snapped/scrollable state |
| generated `::scroll-button()` / `::scroll-marker` | No | carousel enhancement |
| `focusgroup` | No for Firefox 140 ESR | emerging keyboard group navigation |
| `reading-flow` / `reading-order` | No | experimental sequential navigation ordering |
| media state pseudo-classes | No for Firefox 140 ESR | playback styling; Firefox 150+ |
| cross-document View Transitions | No for Firefox 140 ESR | MPA navigation polish |
| scroll-driven animations | No | decoration only |
| container style queries | No/partial for conservative baseline | newer custom-property-derived component styling |
| `@scope` | Verify newer-browser support | selector scoping enhancement |
| typed `attr()` | No/verify | newer attribute-to-CSS value flow |
| CSS `if()` | No | experimental/watchlist |
| CSS custom `@function` | No | experimental author-defined value functions; Chromium 139+, no normal Firefox support at snapshot |
| native masonry/Grid Lanes | No | evolving/watchlist |
| Declarative Partial Updates | No | research/future server-stream patching |
| `text-fit` | No for Firefox 140 ESR | newer presentation enhancement |
| native tooltip proposals | No | watchlist |

## Meaning of labels

**Yes** — may participate in core functionality after product-specific testing.

**Polish** — may improve motion/presentation; losing it cannot remove a task.

**Conditional** — the primitive exists but semantics, privacy, accessibility, gesture behavior or interoperability decide whether it is appropriate.

**No** — keep a baseline path that does not depend on it.

## Baseline warning

A current MDN **Baseline 2026** badge means current mainstream releases converge; it does **not** prove support in Tor Browser's Firefox 140 ESR engine. Compare exact landing versions and test the actual Tor Browser release.
