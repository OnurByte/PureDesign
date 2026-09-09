# PureDesign

**Build interfaces that look like they should need JavaScript — using HTML and CSS instead.**

PureDesign is a practical knowledge base of modern HTML, CSS, native browser features, real URLs/forms, and server-rendered patterns for building rich application-like interfaces with **zero client-side JavaScript**.

The challenge is intentional: if a UI normally reaches for click handlers, DOM state, resize listeners, scroll listeners, custom widget code, hydration, or a frontend runtime, PureDesign asks whether the browser can already do it declaratively.

## The rule

```text
client-side JavaScript = 0
```

No inline scripts. No modules. No event-handler attributes. No hydration runtime. No JavaScript polyfill used to make a pattern work. No "JS is only an enhancement" exception inside a PureDesign implementation.

A backend may be written in any language or runtime. The restriction is on code executed as JavaScript in the browser.

If an interaction cannot be implemented with semantic HTML, CSS, browser-owned state, native controls, URLs/forms, or server-rendered responses, it is **outside the PureDesign solution space**. Document the limitation instead of silently adding JavaScript.

## What is the point?

PureDesign collects techniques for UI that can initially look impossible without JavaScript:

- dropdown and action menus;
- dialogs and confirmation flows;
- accordions and disclosures;
- tabs and URL-backed panels;
- server-backed multi-step forms;
- hierarchical file/folder browsers and native directory uploads;
- bulk-selection and bulk-action workflows;
- server-rendered inline preview/result panels through named browsing contexts;
- bounded image coordinate submission with an accessible fallback;
- responsive navigation;
- sticky application shells and action bars;
- responsive and context-aware components without resize observers;
- form validation and multi-action forms;
- selectable cards;
- search, filtering, sorting, and pagination;
- carousels, URL-addressable slideshows, and snap-based scrollers;
- current/sticky/scroll-derived presentation and reading progress;
- theme and user-preference adaptation;
- native media previews and controls;
- rich native selects where browser support permits them;
- deep links and exact-text highlighting;
- modern transitions and micro-interactions where browser support permits them.

The browser owns as much transient UI state as possible:

```text
open / closed / focus state     -> browser primitives
form state                      -> native controls
navigation state                -> URLs, links and forms
layout and responsive state     -> CSS layout engine
scroll behavior/state           -> browser and CSS
user/device preferences         -> CSS media features
application/durable state       -> server
presentation                    -> CSS
client-side JavaScript          -> forbidden
```

## This is not a framework

PureDesign is not a package, component library, stylesheet, build system, or frontend runtime. There is nothing to install.

It is a reference you can use while building your own UI:

1. Find the UI you want in [`patterns/`](patterns/).
2. Read the small browser capabilities linked from that pattern in [`primitives/`](primitives/).
3. Check [`compatibility/`](compatibility/) before depending on newer features.
4. Adapt the HTML/CSS/server behavior to your own project.

You can use it manually or give the repository to an AI coding agent.

## Quick start

| You want to build | Start here |
|---|---|
| Dropdown/action menu | [`patterns/dropdown-action-menu.md`](patterns/dropdown-action-menu.md) |
| Modal confirmation | [`patterns/modal-confirmation.md`](patterns/modal-confirmation.md) |
| Responsive navigation | [`patterns/responsive-navigation.md`](patterns/responsive-navigation.md) |
| URL-backed tabs | [`patterns/url-tabs.md`](patterns/url-tabs.md) |
| Multi-step wizard/form | [`patterns/server-backed-multi-step-form.md`](patterns/server-backed-multi-step-form.md) |
| Hierarchical file browser | [`patterns/hierarchical-file-browser.md`](patterns/hierarchical-file-browser.md) |
| Directory upload | [`patterns/directory-upload-form.md`](patterns/directory-upload-form.md) |
| Bulk actions | [`patterns/server-backed-bulk-actions.md`](patterns/server-backed-bulk-actions.md) |
| Inline server preview/result | [`patterns/server-backed-inline-result-panel.md`](patterns/server-backed-inline-result-panel.md) |
| Image coordinate picker | [`patterns/server-image-coordinate-picker.md`](patterns/server-image-coordinate-picker.md) |
| Search | [`patterns/server-search-form.md`](patterns/server-search-form.md) |
| Filter / sort / paginate | [`patterns/server-filter-sort-pagination.md`](patterns/server-filter-sort-pagination.md) |
| Sticky Save/Publish actions | [`patterns/detached-form-actions.md`](patterns/detached-form-actions.md) |
| Draft vs Publish form | [`patterns/draft-vs-publish-form.md`](patterns/draft-vs-publish-form.md) |
| Selectable cards | [`patterns/selectable-cards.md`](patterns/selectable-cards.md) |
| Validation feedback | [`patterns/validation-feedback.md`](patterns/validation-feedback.md) |
| Responsive card/file grid | [`patterns/responsive-card-grid.md`](patterns/responsive-card-grid.md) |
| Mobile app-like shell | [`patterns/mobile-app-shell.md`](patterns/mobile-app-shell.md) |
| Long server-rendered list | [`patterns/long-server-rendered-list.md`](patterns/long-server-rendered-list.md) |
| Carousel | [`patterns/carousel.md`](patterns/carousel.md) |
| URL-addressable slideshow | [`patterns/url-slideshow.md`](patterns/url-slideshow.md) |
| Scroll edge cues | [`patterns/scroll-edge-affordance.md`](patterns/scroll-edge-affordance.md) |
| Reading progress | [`patterns/reading-progress.md`](patterns/reading-progress.md) |
| Rich native select | [`patterns/rich-native-select.md`](patterns/rich-native-select.md) |
| Native media preview | [`patterns/native-media-preview.md`](patterns/native-media-preview.md) |
| Theme switching | [`patterns/theme-switcher.md`](patterns/theme-switcher.md) |
| Exact-passage deep links | [`patterns/citable-text-deep-links.md`](patterns/citable-text-deep-links.md) |

## Example: dropdown without JavaScript

A typical application would attach a click listener, toggle state, handle outside clicks, and manage Escape. The browser can own that state with Popover:

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

No script keeps the menu open or closed. The browser does it. Navigation stays a real link and the destructive action stays a real form submission.

See [`patterns/dropdown-action-menu.md`](patterns/dropdown-action-menu.md).

## Example: sticky Save button outside its form

A visually detached action bar does not need a click handler or DOM lookup:

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

The HTML `form` attribute associates the button with the distant form.

See [`patterns/detached-form-actions.md`](patterns/detached-form-actions.md) and [`primitives/form-owner-attribute.md`](primitives/form-owner-attribute.md).

## Example: responsive layout without measuring elements

Do not measure component width in JavaScript just to select a layout. Let the component respond to its own container:

```css
.card-list {
  container-type: inline-size;
}

.card {
  display: grid;
  gap: 1rem;
}

@container (width >= 40rem) {
  .card {
    grid-template-columns: 10rem 1fr auto;
  }
}
```

See [`patterns/responsive-component.md`](patterns/responsive-component.md) and [`primitives/container-size-queries.md`](primitives/container-size-queries.md).

## How the repository is organized

```text
PureDesign/
├── README.md          # entry point for people and AI
├── AGENTS.md          # strict instructions for coding agents
├── CONTRIBUTING.md    # contribution/research contract
├── principles/        # architecture, state ownership and hard boundaries
├── patterns/          # complete reusable UI compositions
├── primitives/        # one browser/platform capability per file
└── compatibility/     # support boundaries and zero-JS testing
```

### `patterns/`

Start here when you have an actual UI problem. A pattern composes multiple platform capabilities into something directly useful.

### `primitives/`

Each file explains one HTML/CSS/browser capability, its semantics, limitations, compatibility, and appropriate use.

Examples:

- [`primitives/popover.md`](primitives/popover.md)
- [`primitives/dialog.md`](primitives/dialog.md)
- [`primitives/details.md`](primitives/details.md)
- [`primitives/form-owner-attribute.md`](primitives/form-owner-attribute.md)
- [`primitives/native-validation.md`](primitives/native-validation.md)
- [`primitives/container-size-queries.md`](primitives/container-size-queries.md)
- [`primitives/name-only-container-queries.md`](primitives/name-only-container-queries.md)
- [`primitives/named-browsing-context-targets.md`](primitives/named-browsing-context-targets.md)
- [`primitives/position-sticky.md`](primitives/position-sticky.md)
- [`primitives/scroll-snap.md`](primitives/scroll-snap.md)
- [`primitives/anchor-positioning.md`](primitives/anchor-positioning.md)
- [`primitives/anchored-container-queries.md`](primitives/anchored-container-queries.md)
- [`primitives/render-blocking-expect.md`](primitives/render-blocking-expect.md)
- [`primitives/at-rule-feature-detection.md`](primitives/at-rule-feature-detection.md)
- [`primitives/native-media-controls.md`](primitives/native-media-controls.md)

### `principles/`

Use these when deciding whether a technique belongs in PureDesign at all:

- [`principles/state-ownership.md`](principles/state-ownership.md)
- [`principles/semantic-html-first.md`](principles/semantic-html-first.md)
- [`principles/progressive-enhancement.md`](principles/progressive-enhancement.md)
- [`principles/server-authoritative-state.md`](principles/server-authoritative-state.md)
- [`principles/accessibility-and-input.md`](principles/accessibility-and-input.md)
- [`principles/hard-boundaries.md`](principles/hard-boundaries.md) — explicit cases that require a different interaction model, a server roundtrip, or an unsupported verdict.

### `compatibility/`

New browser features are useful, but a shiny syntax is not automatically safe to depend on.

- [`compatibility/feature-matrix.md`](compatibility/feature-matrix.md) — core vs progressive/experimental classification.
- [`compatibility/tor-browser-firefox-esr.md`](compatibility/tor-browser-firefox-esr.md) — conservative Tor Browser / Firefox ESR boundary.
- [`compatibility/testing.md`](compatibility/testing.md) — testing protocol with scripting disabled.

Experimental features may add polish or unlock future patterns, but must not be presented as broadly available when they are not.

## Using PureDesign with AI

PureDesign is deliberately split into small files so coding agents do not need the entire repository in context.

Give the agent [`AGENTS.md`](AGENTS.md) as its contract, then let it retrieve only the matching pattern and its linked primitives. If a requested behavior starts requiring client-side event/data plumbing, check [`principles/hard-boundaries.md`](principles/hard-boundaries.md) before inventing CSS state machinery.

Example prompt:

```text
Use the PureDesign repository as the UI reference for this task.
Read AGENTS.md first.

Client-side JavaScript is forbidden. Do not add scripts, event handlers,
hydration, JavaScript polyfills, or a client runtime.

Find the closest pattern in patterns/, follow only its required primitive
and compatibility links, and implement the requested UI using semantic HTML,
CSS, native browser behavior, real URLs/forms, and server-rendered state.

If the requested behavior cannot be achieved inside those constraints, say so
instead of adding JavaScript.
```

For a narrower task:

```text
Build a file action menu using PureDesign.
Start with patterns/dropdown-action-menu.md.
Client-side JavaScript is forbidden.
Follow only the primitive and compatibility files required by that pattern.
```

Recommended retrieval flow:

```text
UI problem
  -> patterns/<matching-pattern>.md
      -> primitives/<required-capability>.md
      -> compatibility/<target>.md when needed
      -> principles/hard-boundaries.md if native/server composition runs out
```

## Design rules

PureDesign prefers semantic HTML over fake widgets, browser-owned state over custom state machines, native controls over reimplementations, real links/forms over client routing, URL/server state over hidden client state, and CSS layout engines over manual measurements.

PureDesign does **not** accept:

- `<script>` or JavaScript modules in an implementation;
- inline JavaScript event attributes such as `onclick`;
- hydration or a browser-side runtime;
- JavaScript polyfills used to provide required behavior;
- click handlers that toggle classes/state;
- JavaScript routing around normal links/forms;
- resize/scroll listeners used for UI behavior;
- a JS library used only because a native HTML/CSS primitive was overlooked;
- calling an implementation "PureDesign" when it requires JavaScript to function.

The point is not merely graceful degradation with JavaScript disabled. **The implementation itself is JavaScript-free.**

## Browser target

The compatibility documentation currently uses **Tor Browser 15.0.21 / Firefox 140.15 ESR** as a conservative reference target while also documenting newer and experimental platform capabilities.

Modern features can still be researched and catalogued, but their support status must remain explicit.

## Contributing

Contributions are welcome. Useful additions include overlooked native browser primitives, unusual HTML/CSS compositions, accessibility findings, compatibility research, browser-version notes, and genuinely useful interfaces that appear to require JavaScript but do not.

Read [`CONTRIBUTING.md`](CONTRIBUTING.md) for the research, compatibility, accessibility and security checklist.

Keep contributions atomic:

1. architectural rules -> `principles/`;
2. one platform capability -> `primitives/`;
3. reusable UI composition -> `patterns/`;
4. browser support/testing -> `compatibility/`;
5. link related files instead of duplicating documentation;
6. separate conservative baseline behavior from experimental features;
7. never solve a PureDesign pattern by adding client-side JavaScript.

## License

PureDesign is released under the [0BSD License](LICENSE).

You may use, copy, modify, redistribute, fork, or include it in commercial projects without an attribution requirement. See [`LICENSE`](LICENSE) for the exact terms.
