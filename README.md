# PureDesign

**Modern web UI with zero client-side JavaScript.**

PureDesign is a research-backed collection of patterns for building interfaces that feel like JavaScript applications while keeping behavior in native HTML, CSS, browser state, and server-rendered navigation.

The core idea is simple:

```text
Ephemeral UI state  -> browser-native HTML state
Form state          -> native form controls + constraint validation
Application state   -> URL / HTTP / server
Presentation        -> CSS
Client-side JS      -> 0
```

This repository was assembled from a deep pass over modern HTML/CSS platform features, GitHub projects and gists, GitHub discussions, and smaller Reddit threads—including useful projects that have received relatively little attention.

## Why this exists

A no-JS interface does not have to feel like a static 2005 document. Modern browsers already provide many of the primitives frontend JavaScript used to recreate manually:

- disclosure and accordions via `<details>` / `<summary>`
- floating menus via the Popover API
- modal semantics via `<dialog>`
- state propagation via `:has()`
- form state via `:checked`, `:user-valid`, and `:user-invalid`
- URL-driven state via `:target`
- keyboard focus via `:focus-visible` / `:focus-within`
- scrolling interactions via CSS scroll snap
- enter/exit polish via transitions, `@starting-style`, and discrete transitions
- server state via ordinary links, forms, redirects, and server-rendered HTML

The design rule is not “do JavaScript in CSS.” It is:

> Find the browser primitive that already owns the interaction, let HTML expose its state, let CSS render that state, and send real application state back to the server.

## Repository map

- [`docs/patterns.md`](docs/patterns.md) — the main no-JS UI architecture and component patterns
- [`docs/hidden-gems.md`](docs/hidden-gems.md) — small GitHub/Reddit findings worth studying
- [`docs/compatibility.md`](docs/compatibility.md) — progressive-enhancement rules, including Tor Browser / Firefox ESR considerations
- [`examples/index.html`](examples/index.html) — a small zero-JS UI playground
- [`examples/styles.css`](examples/styles.css) — all interaction styling for the demo

## The state model

```text
                    BROWSER STATE
                         |
       +-----------------+------------------+
       |                 |                  |
    :checked           :open          :popover-open
       |                 |                  |
       +-----------------+------------------+
                         |
                       :has()
                         |
                         v
                        CSS
                         |
                visual interaction


User action requiring durable state
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

## Practical mapping

| UI problem | Prefer | Avoid making core behavior depend on |
|---|---|---|
| Accordion | `<details>` / `<summary>` | checkbox hacks |
| Dropdown / action menu | `popover` | hand-written positioning JS |
| Selection / toggle | real radio / checkbox | fake div state |
| Parent visual state | `:has()` | JS class toggling |
| Form feedback | native constraints + `:user-invalid` | custom validation state machines |
| Tabs / filters | server URL state or `:target` when appropriate | SPA-only state |
| Carousel | horizontal overflow + scroll snap | drag libraries as a requirement |
| Theme | server preference + `color-scheme`; local radio state when temporary | mandatory localStorage JS |
| Floating UI | normal positioning, enhanced with CSS Anchor Positioning | positioning libraries as a baseline |
| Modal | `<dialog>` where the target browser supports the required invocation path | checkbox-as-modal semantics |
| Motion | CSS transitions / `@starting-style` | animation being required for functionality |

## Three rules

1. **Semantic HTML first.** Use a disclosure as a disclosure, checkbox as a checkbox, button as a button.
2. **Functionality must survive unsupported CSS.** New CSS should add polish or positioning—not decide whether the product works.
3. **Server-render durable state.** Sorting, filtering, auth, CRUD, preferences, pagination, search, uploads, and other authoritative application state belong in URLs/forms/server responses.

## Browser target philosophy

PureDesign separates features into three tiers:

- **Core:** widely available primitives that are safe to build functionality on.
- **Polish:** unsupported browsers lose animation or visual refinement, not behavior.
- **Experimental enhancement:** newer platform features such as CSS Anchor Positioning, scroll-driven animation, or cross-document view transitions must never be the only path to a task.

See [`docs/compatibility.md`](docs/compatibility.md) for the detailed model.

## Sources

The research includes MDN/browser release notes plus smaller community examples such as:

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

More detail and the lessons extracted from each source are in [`docs/hidden-gems.md`](docs/hidden-gems.md).

## License

No license has been selected yet.
