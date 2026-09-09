# PureDesign

**Build modern, application-like web interfaces with semantic HTML, CSS, native browser features, real URLs/forms, and server-rendered state — without requiring client-side JavaScript for core behavior.**

PureDesign is a practical reference for developers **and AI coding agents**. It collects browser capabilities and reusable UI patterns that can replace common JavaScript glue: dropdown toggles, dialogs, responsive layout logic, form routing, validation helpers, scroll state, theme adaptation, media controls, and more.

It is **not a framework, package, component library, or build system**. There is nothing to install. Open the pattern that matches your problem, follow its primitive links, check compatibility, and use the relevant HTML/CSS/server behavior in your own project.

## Why PureDesign?

A lot of frontend JavaScript exists only to reproduce behavior the browser already knows how to provide.

PureDesign starts with a different ownership model:

```text
open / focus / interaction state -> browser
form state                       -> native controls
navigation state                 -> URL / link / form
layout and responsive state      -> CSS layout engine
scroll state                     -> browser / CSS
user preferences                 -> CSS media features
application and durable state    -> server
presentation                     -> CSS
client-side JavaScript           -> optional enhancement, not core requirement
```

The goal is not "never write JavaScript under any circumstances." The goal is to avoid requiring JavaScript when HTML, CSS, browser state, URLs, forms, or the server already solve the problem well.

## Who is this for?

Use PureDesign if you are:

- building server-rendered applications;
- building sites that must remain usable with JavaScript disabled;
- targeting Tor Browser or conservative Firefox ESR environments;
- trying to reduce hydration, client bundles, dependencies, or frontend runtime complexity;
- building with Laravel, Rails, Django, Phoenix, Go templates, ASP.NET, plain HTML, or any other server-rendered stack;
- using an AI coding agent and want it to prefer platform primitives over unnecessary JavaScript libraries;
- researching modern HTML/CSS features that replace categories of frontend JavaScript.

## Quick start

### 1. Find the UI problem

Start in [`patterns/`](patterns/). Patterns describe complete UI compositions such as a dropdown menu, modal confirmation, responsive grid, search form, carousel, or sticky form actions.

Examples:

| You want to build | Start here |
|---|---|
| Dropdown/action menu | [`patterns/dropdown-action-menu.md`](patterns/dropdown-action-menu.md) |
| Modal confirmation | [`patterns/modal-confirmation.md`](patterns/modal-confirmation.md) |
| Responsive navigation | [`patterns/responsive-navigation.md`](patterns/responsive-navigation.md) |
| Search without client fetching | [`patterns/server-search-form.md`](patterns/server-search-form.md) |
| Filter / sort / paginate | [`patterns/server-filter-sort-pagination.md`](patterns/server-filter-sort-pagination.md) |
| Sticky Save/Publish actions | [`patterns/detached-form-actions.md`](patterns/detached-form-actions.md) |
| Draft vs Publish form | [`patterns/draft-vs-publish-form.md`](patterns/draft-vs-publish-form.md) |
| Selectable cards | [`patterns/selectable-cards.md`](patterns/selectable-cards.md) |
| Validation feedback | [`patterns/validation-feedback.md`](patterns/validation-feedback.md) |
| Responsive card/file grid | [`patterns/responsive-card-grid.md`](patterns/responsive-card-grid.md) |
| Mobile app-like shell | [`patterns/mobile-app-shell.md`](patterns/mobile-app-shell.md) |
| Long server-rendered list | [`patterns/long-server-rendered-list.md`](patterns/long-server-rendered-list.md) |
| Carousel | [`patterns/carousel.md`](patterns/carousel.md) |
| Native media preview | [`patterns/native-media-preview.md`](patterns/native-media-preview.md) |
| Theme switching | [`patterns/theme-switcher.md`](patterns/theme-switcher.md) |
| Exact-passage/deep links | [`patterns/citable-text-deep-links.md`](patterns/citable-text-deep-links.md) |

### 2. Follow only the primitive links you need

Each pattern points to small files in [`primitives/`](primitives/). A primitive documents **one browser/platform capability**.

Examples include:

- [`primitives/popover.md`](primitives/popover.md) — browser-owned popovers;
- [`primitives/dialog.md`](primitives/dialog.md) — native dialogs;
- [`primitives/form-owner-attribute.md`](primitives/form-owner-attribute.md) — controls and submit buttons outside their form;
- [`primitives/native-validation.md`](primitives/native-validation.md) — browser constraint validation;
- [`primitives/container-size-queries.md`](primitives/container-size-queries.md) — component responsiveness without resize listeners;
- [`primitives/position-sticky.md`](primitives/position-sticky.md) — sticky UI without scroll listeners;
- [`primitives/scroll-snap.md`](primitives/scroll-snap.md) — browser-owned scrolling/snapping;
- [`primitives/content-visibility.md`](primitives/content-visibility.md) — progressive render skipping;
- [`primitives/native-media-controls.md`](primitives/native-media-controls.md) — browser media playback controls;
- [`primitives/prefers-reduced-motion.md`](primitives/prefers-reduced-motion.md) — user motion preferences.

Do not copy the whole repository into your mental model or prompt unless you actually need it. PureDesign is intentionally split into small files so humans and AI agents can retrieve only relevant context.

### 3. Check browser support

Before making a newer primitive essential to the UI, check:

- [`compatibility/feature-matrix.md`](compatibility/feature-matrix.md) — what may be core vs progressive/experimental;
- [`compatibility/tor-browser-firefox-esr.md`](compatibility/tor-browser-firefox-esr.md) — conservative Tor Browser / Firefox ESR boundary;
- [`compatibility/testing.md`](compatibility/testing.md) — how to test the result with JavaScript disabled.

A new CSS feature being supported by the latest Chrome or Firefox does **not** automatically make it safe for a conservative browser target.

## Example: a menu without click-handler JavaScript

Instead of writing JavaScript to maintain open/closed state, start with the browser-owned Popover API:

```html
<button type="button" popovertarget="file-actions">
  Actions
</button>

<div id="file-actions" popover>
  <a href="/files/123/download">Download</a>

  <form action="/files/123/delete" method="post">
    <button type="submit">Delete</button>
  </form>
</div>
```

The browser owns the temporary open state. Navigation remains a real link. The destructive action remains a real form submission. Your server still owns durable application state.

For the full composition, read [`patterns/dropdown-action-menu.md`](patterns/dropdown-action-menu.md).

## Example: Save button outside the form

You do not need a click handler just because a sticky action bar lives elsewhere in the DOM:

```html
<form id="profile-form" action="/profile" method="post">
  <label>
    Display name
    <input name="display_name" required>
  </label>
</form>

<footer class="sticky-actions">
  <button type="submit" form="profile-form">Save</button>
</footer>
```

The native `form` attribute associates the button with the form. See [`patterns/detached-form-actions.md`](patterns/detached-form-actions.md) and [`primitives/form-owner-attribute.md`](primitives/form-owner-attribute.md).

## Using PureDesign with AI coding agents

PureDesign is structured so an AI agent can use it without loading a giant style guide into context.

The recommended entry point for agents is [`AGENTS.md`](AGENTS.md).

A useful instruction is:

```text
Use the PureDesign repository as the UI/platform reference for this task.
Read AGENTS.md first.
Then open only the pattern matching the requested UI and the primitive/
compatibility files that pattern links to.

Prefer semantic HTML, native browser state, CSS layout/state, real URLs/forms,
and server-rendered state over client-side JavaScript.
Do not make experimental features the only path to core functionality.
```

You can also give an agent a specific task:

```text
Build a server-rendered file action menu using PureDesign.
Start with patterns/dropdown-action-menu.md and follow only its required links.
The result must remain usable with JavaScript disabled.
```

The repository is organized for selective retrieval:

```text
UI problem
  -> patterns/<matching-pattern>.md
      -> primitives/<required-browser-capability>.md
      -> compatibility/<target>.md when needed
```

## Repository structure

```text
PureDesign/
├── README.md          # human + AI entry point
├── AGENTS.md          # detailed instructions for coding agents
├── principles/        # architectural rules and state ownership
├── patterns/          # complete UI compositions
├── primitives/        # one browser/platform capability per file
└── compatibility/     # browser support and zero-JS testing rules
```

### `principles/`

Use these when deciding **who should own state** and whether a technique belongs in PureDesign at all.

Important starting points:

- [`principles/state-ownership.md`](principles/state-ownership.md)
- [`principles/semantic-html-first.md`](principles/semantic-html-first.md)
- [`principles/progressive-enhancement.md`](principles/progressive-enhancement.md)
- [`principles/server-authoritative-state.md`](principles/server-authoritative-state.md)
- [`principles/accessibility-and-input.md`](principles/accessibility-and-input.md)

### `patterns/`

Use these first when solving an actual product/UI problem. A pattern combines primitives without duplicating their documentation.

### `primitives/`

Use these when you need to understand the exact browser capability, support boundary, semantics, accessibility behavior, or fallback strategy.

### `compatibility/`

Use these before relying on newer browser features for core behavior.

## Core design rules

PureDesign generally prefers:

- semantic elements over `div`-based fake controls;
- native buttons, links, forms, inputs, dialogs, disclosures, and media controls;
- browser-owned ephemeral state over custom state machines;
- real URLs for navigable state;
- GET forms for searchable/filterable URL state where appropriate;
- ordinary form submission for server actions;
- server-rendered current/permission/application state;
- CSS Grid/Flexbox/container queries over measurement scripts;
- capability queries over device sniffing;
- progressive enhancement over mandatory polyfills;
- accessibility and predictable browser behavior over visual cleverness.

PureDesign generally avoids:

- hydration as a requirement for core tasks;
- fake links and buttons;
- hidden-checkbox state-machine hacks when a semantic primitive exists;
- JavaScript whose only job is toggling a class the browser can already derive;
- JavaScript routing around ordinary links/forms;
- resize/scroll listeners used only for layout or presentation that CSS can own;
- experimental CSS as the sole route to an important action;
- claiming a JavaScript polyfill is still a "zero-JS" implementation.

## JavaScript is allowed as enhancement

PureDesign does **not** require your entire application to contain zero JavaScript.

A useful boundary is:

```text
JavaScript unavailable -> core task still works
JavaScript available   -> optional convenience/polish may improve
```

For example, autocomplete, optimistic updates, drag-and-drop, richer client caching, or realtime interfaces may reasonably use JavaScript. The baseline should still be designed deliberately instead of accidentally depending on hydration.

## Conservative browser target

The compatibility documentation currently uses **Tor Browser 15.0.21 / Firefox 140.15 ESR** as a conservative reference target.

That target is intentionally stricter than "latest evergreen browser." Newer features can still be documented and used as progressive enhancements.

See [`compatibility/feature-matrix.md`](compatibility/feature-matrix.md) for the current classification.

## Contributing

Contributions are welcome.

When adding material, keep the repository atomic:

1. Put architectural rules in `principles/`.
2. Put one browser/platform capability per file in `primitives/`.
3. Put complete reusable UI compositions in `patterns/`.
4. Put browser-support/testing policy in `compatibility/`.
5. Link related files instead of copying the same explanation everywhere.
6. Separate mature baseline behavior from progressive or experimental features.
7. Do not require client-side JavaScript for a pattern that is presented as zero-JS core behavior.

## License

PureDesign is released under the [0BSD License](LICENSE).

You may use, copy, modify, redistribute, fork, or include it in commercial projects without an attribution requirement. See [`LICENSE`](LICENSE) for the exact terms.
