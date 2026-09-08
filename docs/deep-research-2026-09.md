# Deep Research — September 2026

This pass extends the original PureDesign research with newer and less-discussed browser primitives that can remove more client-side JavaScript.

The focus is not on novelty for its own sake. Each feature is classified by one question:

> Does it move state, keyboard behavior, positioning, scrolling, rendering, or server updates back into the browser without making the application brittle?

Compatibility snapshot: **2026-09-08**.

---

## 1. `hidden="until-found"`: hidden content that Ctrl+F and fragments can still reveal

This is unusually useful for dense no-JS applications.

```html
<section id="advanced-settings" hidden="until-found">
    <h2>Advanced settings</h2>
    <p>Rarely used settings live here.</p>
</section>
```

Unlike ordinary `hidden`, the browser may reveal this content when:

- the user searches for matching text with Find in Page
- a URL fragment navigates directly to it

Firefox added support in **Firefox 139**, so this is available to a Firefox 140 ESR-based target.

Sources:

- MDN Firefox 139 release notes: https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/139
- MDN hidden attribute reference: https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes/hidden

### Why this matters

A normal collapsed/filtered UI often introduces a JavaScript problem:

```text
content hidden
    -> Ctrl+F cannot reach it
    -> URL anchor cannot reveal it
    -> JS must intercept beforematch/hashchange
```

`hidden="until-found"` lets the browser own the reveal path.

Potential PureDesign uses:

- advanced settings
- long help pages
- archived sections
- collapsed reference material
- search-result detail areas

### Footgun

Do not override it with generic CSS such as:

```css
[hidden] {
    display: none !important;
}
```

That destroys the special behavior. A safer reset is:

```css
[hidden]:where(:not([hidden="until-found"])) {
    display: none !important;
}
```

A small Tailwind-preflight-derived gist preserves exactly this distinction:
https://gist.github.com/vic876vb/cb113ea7eac166c566b21714d53fa9c4

---

## 2. Native multi-action forms: `formaction`, `formmethod`, `form`, `formtarget`

A surprising amount of frontend event routing can be replaced by old, widely-supported HTML.

```html
<form id="file-form" action="/files/save" method="post">
    <input name="name" required>

    <button type="submit">Save</button>

    <button
        type="submit"
        formaction="/files/save-and-close">
        Save and close
    </button>

    <button
        type="submit"
        formaction="/files/preview"
        formmethod="get"
        formtarget="_blank">
        Preview
    </button>
</form>
```

The submitter can override the form's destination and HTTP method without JavaScript.

Controls can also live outside the form visually:

```html
<form id="profile" action="/profile" method="post">
    ...
</form>

<footer class="sticky-actions">
    <button form="profile" type="submit">Save profile</button>
</footer>
```

Sources:

- MDN `<button>`: https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/button
- MDN `form` attribute: https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/form

### What this replaces

```text
click listener
 -> inspect which button
 -> build request
 -> choose endpoint
 -> fetch()
```

with:

```text
native submitter
 -> HTTP
 -> server
```

For server-rendered applications this is a Tier-A pattern and deserves much more attention than it gets.

---

## 3. CSS-native scrollspy: `scroll-target-group` + `:target-current`

This is one of the most direct replacements for `IntersectionObserver`-based UI.

```html
<nav class="toc">
    <a href="#intro">Intro</a>
    <a href="#security">Security</a>
    <a href="#storage">Storage</a>
</nav>

<section id="intro">...</section>
<section id="security">...</section>
<section id="storage">...</section>
```

```css
.toc {
    scroll-target-group: auto;
}

.toc a:target-current {
    font-weight: 700;
    text-decoration: underline;
}
```

The browser tracks which anchor target is current and styles its link.

Source:
https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/scroll-target-group

Standards-position discussion:
https://github.com/mozilla/standards-positions/issues/1251

### Low-visibility implementation worth studying

TingRubato published a small gist combining:

- `scroll-target-group`
- `:target-current`
- CSS Anchor Positioning
- `:has()`

for a moving table-of-contents marker:

https://gist.github.com/TingRubato/5a8474ed70eae1075f4db90211d510d2

The especially interesting idea is to give the current link an anchor name and position one visual indicator against whichever link currently owns that anchor.

### Why this is important

Traditional scrollspy:

```text
IntersectionObserver
 -> calculate active section
 -> remove .active
 -> add .active
```

Native model:

```text
anchor targets + scrolling
 -> browser computes current target
 -> :target-current
 -> CSS
```

This is currently enhancement-only for conservative Firefox/Tor targets.

---

## 4. Browser-generated carousel controls

CSS Overflow Level 5 is turning a plain scroll container into a complete carousel primitive.

New pieces include:

- `::scroll-button()`
- `scroll-marker-group`
- `::scroll-marker-group`
- `::scroll-marker`
- `:target-current`
- `:target-before`
- `:target-after`

MDN guide:
https://developer.mozilla.org/en-US/docs/Web/CSS/Guides/Overflow/Carousels

A future-enhanced carousel can look like:

```css
.carousel {
    display: flex;
    overflow-x: auto;
    scroll-snap-type: x mandatory;
    scroll-marker-group: after;
}

.carousel > article {
    flex: 0 0 100%;
    scroll-snap-align: center;
}

.carousel::scroll-button(left) {
    content: "←" / "Previous";
}

.carousel::scroll-button(right) {
    content: "→" / "Next";
}

.carousel > article::scroll-marker {
    content: "";
    inline-size: .7rem;
    block-size: .7rem;
    border: 1px solid currentColor;
    border-radius: 50%;
}

.carousel > article::scroll-marker:target-current {
    background: currentColor;
}
```

The browser can generate stateful buttons and markers and automatically disable an edge button when scrolling can go no farther.

Chrome's Web UI recap emphasizes that the browser supplies roles/tab behavior for these generated controls:
https://developer.chrome.com/blog/new-in-web-ui-io-2025-recap

### Important design rule

The baseline remains ordinary scroll snap:

```css
.carousel {
    overflow-x: auto;
    scroll-snap-type: x mandatory;
}
```

The generated buttons/markers are enhancement only until the browser matrix supports them.

Reddit edge case: a March 2026 thread asked whether the new carousel primitives make looping automatic. They do not; native controls solve navigation/state, not infinite circular data structures.

https://www.reddit.com/r/css/comments/1ri193f/

---

## 5. `focusgroup`: declarative roving focus and arrow-key navigation

Roving `tabindex` is one of the most repetitive accessibility scripts in component libraries.

The emerging `focusgroup` attribute lets the browser handle:

- arrow-key movement
- a single group entry point
- focus memory
- wrapping
- axis behavior

Example:

```html
<div focusgroup="toolbar wrap" aria-label="Editor actions">
    <button>Bold</button>
    <button>Italic</button>
    <button>Underline</button>
</div>
```

Chrome/Edge 150 shipped the primitive in 2026.

Sources:

- Chrome 150: https://developer.chrome.com/blog/new-in-chrome-150
- WHATWG proposal: https://github.com/whatwg/html/issues/11641
- Edge demo: https://github.com/MicrosoftEdge/Demos/blob/main/focusgroup/tablist.html

### Crucial boundary

`focusgroup` owns **navigation**, not application selection state.

It can remove roving-focus JavaScript from a toolbar or composite widget, but it does not magically make a full tab component switch panels.

This distinction belongs in PureDesign's state model:

```text
keyboard focus movement -> browser
selected application item -> URL/form/server/native control
```

A newer WHATWG issue is already exploring grid navigation and nested controls:
https://github.com/whatwg/html/issues/12776

---

## 6. `interestfor` + `popover="hint"`: declarative tooltip / hovercard direction

Chrome 142 introduced `interestfor` for links and buttons.

Conceptually:

```html
<button interestfor="save-help">Save</button>

<div id="save-help" popover="hint">
    Saves the current document.
</div>
```

The user agent can detect “interest” through pointer hover, keyboard behavior, or touch interaction and apply the default popover behavior.

Source:
https://developer.chrome.com/blog/new-in-chrome-142

Spec discussion:
https://github.com/whatwg/html/issues/10309

Microsoft's tooltip explainer is especially useful because it documents why this matters for accessibility and input handling:
https://github.com/MicrosoftEdge/MSEdgeExplainers/blob/main/CSSTooltipPseudo/explainer.md

### Hidden lesson

CSS-only `:hover` tooltips are easy but usually incomplete:

- keyboard focus may not expose them
- touch behavior is unclear
- dismissal is easy to get wrong
- positioning becomes fragile

`interestfor` is promising because the **input modality problem** moves to the user agent.

For Tor/Firefox ESR, this is future-watchlist material, not core UI.

---

## 7. Customizable native `<select>`

`appearance: base-select` is a major change in how much UI can remain a real `<select>`.

```css
select,
select::picker(select) {
    appearance: base-select;
}
```

The newer model includes:

- rich option content
- `::picker(select)`
- `::picker-icon`
- `::checkmark`
- `:open`
- `:checked`
- `<selectedcontent>`

MDN guide:
https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Forms/Customizable_select

### Excellent low-visibility gist

Ivan Jurković published a **0-star** `select.scss` gist in June 2026 that treats customizable select correctly as progressive enhancement:

https://gist.github.com/ijurko

Its key rule is not the styling. It is the fallback contract:

```text
supports base-select -> branded picker
unsupported          -> ordinary native select
```

### Framework irony

A useful GitHub/Reddit side finding is that the native platform moved faster than some framework validators/hydration assumptions.

Examples:

- Vite/Vue discussion about outdated nesting warnings: https://github.com/vitejs/vite-plugin-vue/discussions/562
- Svelte issue around customizable-select binding: https://github.com/sveltejs/svelte/issues/18347
- Solid discussion around unsupported-browser DOM parsing: https://github.com/solidjs/solid/discussions/2463

This is exactly why PureDesign should treat semantic browser primitives as first-class rather than assume framework abstractions are always ahead of the platform.

Firefox 149 still exposed `base-select` behind preferences and only partial picker styling, so this is not suitable for Firefox 140 ESR core behavior.

Source:
https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/149

---

## 8. Native autocomplete with `<datalist>` — useful but not universally good

For simple suggestion lists:

```html
<label for="city">City</label>
<input id="city" name="city" list="cities">

<datalist id="cities">
    <option value="Bolu">
    <option value="Ankara">
    <option value="Istanbul">
</datalist>
```

This gives a browser-managed typeahead without a combobox library.

MDN:
https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/datalist

### Why it is not a universal replacement

MDN currently flags `<datalist>` as Limited Availability and lists accessibility limitations, including poor styling/high-contrast control and some screen-reader/browser announcement problems.

A Reddit thread that initially celebrated `<datalist>` also contains the useful counterarguments: weak styling, ID/display-value limitations, and inconsistent implementations.

https://www.reddit.com/r/webdev/comments/brnwj9/

### PureDesign rule

Use `<datalist>` for optional suggestions when its UX is acceptable. Do not blindly call it an accessible custom-combobox replacement.

---

## 9. `inert`: disable an entire subtree declaratively

`inert` has been broadly available since 2023.

```html
<section class="billing-panel" inert>
    <input name="card">
    <button>Pay</button>
</section>
```

The subtree is removed from normal interaction/focus behavior.

MDN:
https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes/inert

### Server-rendered use

A server can render inactive workflow stages as inert:

```html
<section @if(!$canEdit) inert @endif>
```

and CSS can make that state visible:

```css
[inert] {
    opacity: .55;
}
```

This is useful for wizard stages, permission-gated panels, and read-only snapshots.

Do not use it merely to visually dim content: inert also changes focus, selection, find-in-page, and accessibility exposure.

---

## 10. Declarative Partial Updates: HTML patching without interaction-time JS

This is the biggest future-facing discovery in this pass.

The WICG proposal introduces out-of-order HTML patching with `<template for>`.

Conceptual example:

```html
<div id="results">
    <?start name="results">Loading…<?end>
</div>

<!-- arrives later in the same stream -->
<template for="results">
    <article>Result One</article>
</template>
```

The patch can be applied declaratively as the HTML stream is parsed—no inline patching script required.

Sources:

- Chrome overview: https://developer.chrome.com/docs/web-platform/declarative-partial-updates
- WICG repository: https://github.com/WICG/declarative-partial-updates
- Patching explainer: https://github.com/WICG/declarative-partial-updates/blob/main/patching-explainer.md

Chrome's documentation explicitly frames this as a way to replace the inline scripts frameworks often inject for out-of-order server streaming.

### Why this is extremely relevant to server-rendered no-JS apps

Today:

```text
slow DB component
      |
      +--> block whole HTML response

or

stream placeholder
      |
      +--> inline JS patches DOM later
```

Proposed native model:

```text
stream shell immediately
      |
      +--> server finishes component later
      |
      +--> <template for> patch arrives
      |
      +--> browser inserts it
```

That potentially brings React-style out-of-order streaming to a zero-client-JS server architecture.

### Current status

This is **not** a Tor/Firefox ESR primitive. Chrome documentation in September 2026 shows out-of-order streaming support in Chromium 150-class browsers, while other parts of Declarative Partial Updates remain experimental/future work.

The proposal also contains future directions for:

- declarative route matching
- same-document navigations
- native fragment includes (`<template src>` style ideas)

Those are research targets, not production assumptions.

### Community precursor: PHOOOS

Before `<template for>`, the PHOOOS technique explored Declarative Shadow DOM as a no-JS out-of-order streaming trick.

Low-visibility Reddit threads:

- https://www.reddit.com/r/webdev/comments/1bq9l84/ — ~3 votes when posted
- https://www.reddit.com/r/webdev/comments/1c9jgzw/ — later follow-up

The important historical point is that the platform is now standardizing a cleaner version of a problem community experiments were already trying to solve.

---

## 11. `popover="hint"` is not the same thing as a click menu

Modern Popover has three modes with different state semantics:

```text
auto   -> light-dismiss; interacts with auto stack
hint   -> lightweight hint stack; does not normally close unrelated auto popovers
manual -> stays until explicitly controlled
```

MDN:
https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes/popover

This matters for layered interfaces such as:

```text
account menu (auto)
    +-- help tooltip (hint)
```

A tooltip should not necessarily close the menu that contains its trigger.

PureDesign should treat popover mode as part of state semantics, not as a styling option.

---

## 12. The next tooltip primitive may be `::tooltip`

Microsoft Edge's explainer explores a `::tooltip` pseudo-element for styling browser-native `title` tooltips while leaving:

- input handling
- positioning
- accessibility
- timing

with the user agent.

Explainer:
https://github.com/MicrosoftEdge/MSEdgeExplainers/blob/main/CSSTooltipPseudo/explainer.md

This is still a proposal, but it shows the direction of travel:

```text
custom JS tooltip library
        ↓
popover + anchor + interestfor
        ↓
possibly native styleable tooltip pseudo
```

Do not use this in production yet; keep it in the watchlist.

---

## 13. Browser-native responsive text sizing: `text-fit`

Chrome 150 introduced `text-fit`, allowing text to fill a box without measuring text in JavaScript.

Source:
https://developer.chrome.com/blog/new-in-chrome-150

This replaces a narrower but common class of scripts:

```text
measure text
 -> binary-search font size
 -> resize observer
 -> set inline font-size
```

It is presentation rather than state, but it fits PureDesign's broader principle:

> Before measuring layout in JavaScript, check whether layout itself can own the problem.

Enhancement only for conservative targets.

---

# New architecture map

The deeper pass expands PureDesign's ownership model:

```text
DISCLOSURE STATE        -> details/open
OVERLAY STATE           -> popover/dialog
SELECTION STATE         -> radio/checkbox/select
FORM ROUTING            -> form/action + submitter overrides
VALIDATION STATE        -> native constraints + :user-*
FIND/REVEAL STATE       -> hidden=until-found
SCROLL POSITION STATE   -> scroll snap / target-current
KEYBOARD GROUP NAV      -> focusgroup (emerging)
HOVER/INTEREST STATE    -> interestfor (emerging)
DURABLE APP STATE       -> URL / HTTP / server
ASYNC SERVER PATCHING   -> template-for (emerging)
PRESENTATION            -> CSS
```

The recurring pattern is not “CSS can do JavaScript.”

It is:

> More kinds of state are becoming first-class browser state.

---

# Best new findings by practical value

## Useful now for Firefox/Tor-ESR-style targets

1. `hidden="until-found"`
2. native multi-action forms (`formaction`, `formmethod`, `form`)
3. `inert` for server-rendered inactive subtrees
4. grouped `<details name>` (already in Firefox 130+)
5. normal scroll snap as the fallback for carousel/bottom-sheet interactions

## High-value progressive enhancements

1. `scroll-target-group` + `:target-current`
2. `::scroll-button()` / `::scroll-marker`
3. customizable `<select>`
4. CSS Anchor Positioning

## Watch closely

1. Declarative Partial Updates / `<template for>`
2. `focusgroup`
3. `interestfor`
4. `::tooltip`
5. declarative same-document routing in the DPU proposal

---

# Research sources worth preserving

Small or unusually useful sources discovered in this pass:

- TingRubato — moving CSS-native TOC marker: https://gist.github.com/TingRubato/5a8474ed70eae1075f4db90211d510d2
- ijurko — 0-star progressive customizable-select gist: https://gist.github.com/ijurko
- PHOOOS low-visibility discussion: https://www.reddit.com/r/webdev/comments/1bq9l84/
- PHOOOS follow-up: https://www.reddit.com/r/webdev/comments/1c9jgzw/
- Customizable-select edge-case discussion: https://www.reddit.com/r/webdev/comments/1muj5us/
- CSS carousel looping limitations: https://www.reddit.com/r/css/comments/1ri193f/
- Declarative Partial Updates community reaction: https://www.reddit.com/r/webdev/comments/1tma96z/
- Microsoft focusgroup demo: https://github.com/MicrosoftEdge/Demos/blob/main/focusgroup/tablist.html
- WICG Declarative Partial Updates: https://github.com/WICG/declarative-partial-updates

The repository should continue preferring small sources that expose a reusable architectural idea over large collections that merely contain many components.
