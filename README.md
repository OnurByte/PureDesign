# PureDesign

**Modern web UI with zero client-side JavaScript.**

PureDesign is a research-backed collection of patterns for building interfaces that feel like JavaScript applications while keeping behavior in native HTML, CSS, browser state, URLs, forms, and server-rendered navigation.

The project is deliberately not “CSS doing JavaScript.” The goal is to identify which state already belongs to the browser and let the platform own it.

```text
Ephemeral UI state     -> native HTML state
Form state             -> native controls + constraint validation
Navigation state       -> URL / fragments
Scroll state           -> browser scrolling / snapping / target tracking
Keyboard group state   -> browser focus primitives
Application state      -> HTTP / server
Presentation           -> CSS
Client-side JS         -> 0
```

## Why this exists

Modern browsers already provide many primitives frontend JavaScript used to recreate manually:

- disclosure and accordions via `<details>` / `<summary>` / `<details name>`
- floating menus via the Popover API
- modal semantics via `<dialog>`
- state propagation via `:has()`
- form state via `:checked`, `:user-valid`, and `:user-invalid`
- multiple form actions via `formaction`, `formmethod`, and `form`
- URL-driven state via `:target`
- findable collapsed content via `hidden="until-found"`
- subtree deactivation via `inert`
- keyboard focus via `:focus-visible` / `:focus-within`
- scrolling interactions via CSS Scroll Snap
- newer scrollspy via `scroll-target-group` + `:target-current`
- newer browser-generated carousel controls via `::scroll-button()` / `::scroll-marker`
- native suggestion lists via `<datalist>` where its accessibility tradeoffs are acceptable
- enter/exit polish via transitions, `@starting-style`, and discrete transitions
- server state via ordinary links, forms, redirects, and server-rendered HTML

The deeper September 2026 pass also tracks emerging primitives that move even more frontend machinery into the browser:

- `focusgroup` for declarative arrow-key / roving-focus navigation
- `interestfor` + `popover="hint"` for declarative interest/tooltip behavior
- customizable `<select>` via `appearance: base-select`
- Declarative Partial Updates / `<template for>` for out-of-order server HTML patching without interaction-time JavaScript

These newer features are documented as research/enhancement targets, not blindly treated as universal baseline features.

## Repository map

- [`docs/patterns.md`](docs/patterns.md) — the main no-JS UI architecture and component patterns
- [`docs/hidden-gems.md`](docs/hidden-gems.md) — small GitHub/Reddit findings worth studying
- [`docs/deep-research-2026-09.md`](docs/deep-research-2026-09.md) — deeper pass covering new browser primitives, low-visibility gists, and emerging HTML/CSS
- [`docs/compatibility.md`](docs/compatibility.md) — progressive-enhancement rules, including Tor Browser / Firefox ESR considerations
- [`examples/index.html`](examples/index.html) — original zero-JS UI playground
- [`examples/styles.css`](examples/styles.css) — original demo styles
- [`examples/native-deep.html`](examples/native-deep.html) — deeper native primitive demo
- [`examples/native-deep.css`](examples/native-deep.css) — progressive enhancement for the deeper demo

## The state model

```text
                       BROWSER STATE
                            |
      +----------+----------+-----------+-------------+
      |          |          |           |             |
   :checked    :open   :popover-open   :target   scroll/current
      |          |          |           |             |
      +----------+----------+-----------+-------------+
                            |
                          :has()
                            |
                            v
                           CSS
                            |
                    visual interaction


Durable user action
       |
       v
link / native form
       |
       v
      HTTP
       |
       v
application server
       |
       v
rendered HTML
```

The September 2026 research adds two more important ownership categories:

```text
find/reveal state       -> hidden="until-found"
keyboard group nav      -> focusgroup (emerging)
interest/hover state    -> interestfor (emerging)
async server patching   -> <template for> (emerging)
```

## Practical mapping

| UI problem | Prefer | Avoid making core behavior depend on |
|---|---|---|
| Accordion | `<details>` / `<summary>` / grouped `name` | checkbox hacks |
| Dropdown / action menu | `popover` | hand-written overlay state |
| Selection / toggle | real radio / checkbox / select | fake div state |
| Parent visual state | `:has()` | JS class toggling |
| Form feedback | native constraints + `:user-invalid` | custom touched-state machines |
| Multi-action form | `formaction` / `formmethod` / submitter values | click router + `fetch()` |
| Hidden but searchable content | `hidden="until-found"` | JS hash/find reveal logic |
| Tabs / filters | server URL state or `:target` when appropriate | SPA-only state |
| Scrollspy | ordinary anchors; enhance with `scroll-target-group` | IntersectionObserver as baseline |
| Carousel | horizontal overflow + scroll snap; enhance with CSS carousel controls | drag library as requirement |
| Theme | server preference + `color-scheme`; local radio state when temporary | mandatory localStorage JS |
| Floating UI | normal positioning, enhanced with CSS Anchor Positioning | positioning library as baseline |
| Modal | `<dialog>` where target invocation path is supported | checkbox-as-modal semantics |
| Disabled subtree | server-rendered `inert` | manually disabling every descendant |
| Lightweight suggestions | `<datalist>` when appropriate | assuming every combobox needs a framework |
| Motion | CSS transitions / `@starting-style` | animation being required for functionality |

## Five rules

1. **Semantic HTML first.** Use a disclosure as a disclosure, checkbox as a checkbox, link as navigation, and button as an action.
2. **Let the browser own ephemeral state.** Do not mirror browser state into arbitrary classes if CSS can observe the real state.
3. **Functionality must survive unsupported CSS.** New CSS should add polish, navigation help, or positioning—not decide whether the task exists.
4. **Server-render durable state.** Sorting, filtering, auth, CRUD, preferences, pagination, search, uploads, and permissions belong in URLs/forms/server responses.
5. **Separate shipped features from future platform direction.** `hidden="until-found"` and `formaction` are not in the same compatibility category as `focusgroup` or Declarative Partial Updates.

## Browser target philosophy

PureDesign separates features into three tiers:

- **Core:** features verified in the declared browser baseline.
- **Polish:** unsupported browsers lose animation or visual refinement, not behavior.
- **Experimental enhancement:** newer platform features must never be the only path to a task.

For the current conservative reference target, Tor Browser stable is tracked against its exact Firefox ESR base instead of assuming that whatever current Firefox supports is available in Tor.

See [`docs/compatibility.md`](docs/compatibility.md) for the detailed model and [`docs/deep-research-2026-09.md`](docs/deep-research-2026-09.md) for the newest findings.

## Particularly useful research sources

The research includes browser release notes/spec work plus small community examples that expose reusable ideas:

- Adam Bien — [unscripted](https://github.com/AdamBien/unscripted)
- YieldRay — [css-only-demo.html](https://gist.github.com/YieldRay/3d965bf568332a25c38f8c00fb79285e)
- viliket — [pure-web-bottom-sheet](https://github.com/viliket/pure-web-bottom-sheet)
- Johannes Mutter — [AnchorPop](https://github.com/johannesmutter/anchorpop)
- TeamDijon — [details-animation-support.css](https://gist.github.com/TeamDijon)
- webfactory — [dialog-utils](https://github.com/webfactory/dialog-utils)
- Demetris — [Omni Carousel](https://github.com/demetris/omni-carousel)
- Digicreon — [µCSS](https://github.com/Digicreon/muCSS)
- Pico CSS — [Discussion #343](https://github.com/picocss/pico/discussions/343)
- blackspike — [popover-menu.css](https://gist.github.com/blackspike)
- TingRubato — [CSS-native TOC marker gist](https://gist.github.com/TingRubato/5a8474ed70eae1075f4db90211d510d2)
- ijurko — [0-star customizable-select gist collection](https://gist.github.com/ijurko)
- WICG — [Declarative Partial Updates](https://github.com/WICG/declarative-partial-updates)
- Microsoft Edge — [focusgroup demos](https://github.com/MicrosoftEdge/Demos/blob/main/focusgroup/tablist.html)

More detail and caveats are preserved in the docs instead of treating any repo as a dependency recommendation.

## License

No license has been selected yet.
