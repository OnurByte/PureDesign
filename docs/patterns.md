# PureDesign Patterns

This document turns the research into a practical architecture for building modern-feeling interfaces with **zero client-side JavaScript**.

## 1. The fundamental model

Do not treat CSS as a replacement programming language for JavaScript. Divide state by ownership:

```text
Ephemeral interaction state  -> browser
Form state                   -> native form controls
Navigation state             -> URL
Durable application state    -> server
Visual state                 -> CSS
```

A typical server-rendered application becomes:

```text
button / link / form
        |
        v
       HTTP
        |
        v
      server
        |
        v
   rendered HTML
        |
        v
       CSS
```

Local interactions that do not require server data should stay inside browser-native primitives.

---

## 2. Accordions and disclosures

Use semantic disclosure elements:

```html
<details>
    <summary>Security</summary>
    <div class="panel">
        Security settings...
    </div>
</details>
```

For accordion-like groups, modern browsers can coordinate disclosures through the `name` attribute:

```html
<details name="settings">
    <summary>Security</summary>
    <div class="panel">...</div>
</details>

<details name="settings">
    <summary>Storage</summary>
    <div class="panel">...</div>
</details>
```

### Why this is better than the checkbox hack

A checkbox has checkbox semantics. A disclosure has disclosure semantics. Using `<details>` gives the browser ownership of:

- open/closed state
- keyboard interaction
- accessibility semantics
- state exposure through `open`

### Animation

Treat animation as progressive enhancement:

```css
@media (prefers-reduced-motion: no-preference) {
    details {
        transition: background 160ms ease;
    }

    @supports (interpolate-size: allow-keywords) {
        details {
            interpolate-size: allow-keywords;
        }

        details::details-content {
            block-size: 0;
            opacity: 0;
            overflow: clip;
            transition:
                block-size 180ms ease,
                opacity 140ms ease,
                content-visibility 180ms allow-discrete;
        }

        details[open]::details-content {
            block-size: auto;
            opacity: 1;
        }
    }
}
```

If this enhancement is unsupported, the disclosure must still work normally.

### UX caveat

Auto-closing accordion groups can shift the document substantially on small screens. Native does not automatically mean good UX; test long content and scroll position.

---

## 3. Dropdowns and action menus with Popover

A large class of frontend JavaScript can be replaced by declarative popovers:

```html
<button popovertarget="account-menu">
    Account
</button>

<div id="account-menu" popover>
    <a href="/profile">Profile</a>
    <a href="/settings">Settings</a>

    <form method="post" action="/logout">
        <button type="submit">Logout</button>
    </form>
</div>
```

The browser can own:

- open/close state
- top-layer placement
- Escape handling
- light dismiss for auto popovers
- invoker relationship

CSS can style the state directly:

```css
[popover] {
    opacity: 0;
    transform: translateY(-.35rem) scale(.98);
    transition:
        opacity 120ms ease,
        transform 120ms ease,
        display 120ms allow-discrete;
}

[popover]:popover-open {
    opacity: 1;
    transform: none;
}

@starting-style {
    [popover]:popover-open {
        opacity: 0;
        transform: translateY(-.35rem) scale(.98);
    }
}
```

### Positioning strategy

Baseline:

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

Progressively enhance with CSS Anchor Positioning when the browser target supports it.

Do not make the product unusable if anchor positioning is unavailable.

---

## 4. `:has()` as state propagation

One of the most useful modern CSS primitives is `:has()` because it lets a parent react to descendant state.

### Focused field

```css
.field:has(input:focus-visible) {
    border-color: var(--accent);
    box-shadow: 0 0 0 3px var(--focus-ring);
}
```

### Selected card

```html
<label class="plan">
    <input type="radio" name="plan" value="pro">
    <span>Pro</span>
</label>
```

```css
.plan:has(input:checked) {
    border-color: var(--accent);
    background: var(--selected-bg);
}
```

### Invalid form group

```css
.field:has(input:user-invalid) {
    border-color: var(--danger);
}
```

This replaces many cases where JavaScript would otherwise toggle classes such as `.active`, `.selected`, `.invalid`, or `.focused`.

---

## 5. Native form validation

Prefer browser constraint validation before inventing a client state machine.

```html
<label class="field">
    <span>Email</span>
    <input type="email" name="email" required>
</label>
```

```css
input:user-invalid {
    border-color: var(--danger);
}

input:user-valid {
    border-color: var(--success);
}
```

`:user-invalid` is generally preferable to immediately painting every untouched required input as erroneous.

A useful rule:

> Focus is not proof of user error. Validation feedback should follow meaningful user interaction.

Server-side validation remains authoritative.

---

## 6. URL-driven state

The URL is a durable, shareable, browser-native state store.

### Fragment state

```html
<nav class="tabs">
    <a href="#general">General</a>
    <a href="#security">Security</a>
    <a href="#billing">Billing</a>
</nav>

<section id="general" class="tab-panel">...</section>
<section id="security" class="tab-panel">...</section>
<section id="billing" class="tab-panel">...</section>
```

```css
.tab-panel {
    display: none;
}

.tab-panel:target {
    display: block;
}
```

Benefits:

- refresh persistence
- browser back/forward
- deep linking
- bookmarkability
- no JavaScript state synchronization

Use this only where fragment semantics make sense. Do not force `:target` into every tab interface.

### Server URL state

For real application state, query parameters are usually better:

```text
/files?view=grid&sort=size&page=2
```

Server rendering:

```php
$view = request('view', 'list');
```

```html
<body data-view="{{ $view }}">
```

```css
body[data-view="grid"] .files {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(12rem, 1fr));
}

body[data-view="list"] .files {
    display: block;
}
```

This gives durable state without a client framework.

---

## 7. Theme state

Temporary local state can be driven by real radio controls:

```html
<label>
    <input type="radio" name="color-scheme" value="system" checked>
    System
</label>

<label>
    <input type="radio" name="color-scheme" value="light">
    Light
</label>

<label>
    <input type="radio" name="color-scheme" value="dark">
    Dark
</label>
```

```css
:root:has(input[name="color-scheme"][value="light"]:checked) {
    color-scheme: light;
}

:root:has(input[name="color-scheme"][value="dark"]:checked) {
    color-scheme: dark;
}
```

For persistence, move the authoritative preference to the server:

```text
POST /settings/theme
        |
        v
cookie / account preference
        |
        v
<html data-theme="dark">
```

Do not require localStorage JavaScript for a theme to function.

---

## 8. Carousels without carousel JavaScript

A basic usable carousel is a horizontal scroll container:

```html
<div class="carousel" aria-label="Featured items">
    <article>One</article>
    <article>Two</article>
    <article>Three</article>
</div>
```

```css
.carousel {
    display: flex;
    gap: 1rem;
    overflow-x: auto;
    scroll-snap-type: x mandatory;
    scrollbar-gutter: stable;
}

.carousel > * {
    flex: 0 0 min(85%, 24rem);
    scroll-snap-align: start;
}
```

The important architectural lesson from small carousel projects is:

```text
HTML + CSS = usable product
optional JS = enhancement
```

not:

```text
JS = product
noscript = broken fallback
```

---

## 9. Bottom sheets as scrolling systems

A particularly strong community pattern is to model a draggable bottom sheet as a scroll container rather than recreating touch physics in JavaScript.

Conceptually:

```css
.bottom-sheet {
    overflow-y: auto;
    scroll-snap-type: y mandatory;
}

.bottom-sheet__snap {
    scroll-snap-align: start;
}
```

Instead of implementing:

```text
pointermove
velocity calculation
requestAnimationFrame
translateY
snap thresholds
```

you let the browser's scrolling engine provide momentum and snapping.

General lesson:

> When an interaction looks custom, first ask whether the browser already has equivalent physics under another primitive.

Examples:

- bottom sheet -> scrolling
- carousel -> horizontal scrolling
- accordion -> disclosure
- dropdown -> popover
- modal -> dialog

---

## 10. Declarative Shadow DOM

Server-rendered component isolation is possible without calling `attachShadow()` in JavaScript:

```html
<example-menu>
    <template shadowrootmode="open">
        <style>
            :host {
                display: inline-block;
            }
        </style>

        <slot></slot>
    </template>
</example-menu>
```

This is especially interesting for server-generated components where style isolation is valuable but client-side custom-element logic is not required.

Do not introduce Shadow DOM automatically. It changes styling, form, accessibility, and composition boundaries. Use it where isolation buys something concrete.

---

## 11. Dialogs

`<dialog>` gives real modal/dialog semantics.

Modern declarative invocation is moving toward patterns such as:

```html
<button commandfor="delete-dialog" command="show-modal">
    Delete
</button>

<dialog id="delete-dialog">
    <p>Delete this file?</p>

    <button commandfor="delete-dialog" command="close">
        Cancel
    </button>
</dialog>
```

However, support for declarative command invocation is newer than the dialog element itself.

For conservative browser targets, do not make core tasks depend on a declarative invocation feature until the target browser actually ships it.

---

## 12. Motion is responsible for much of the “app feel”

Many interfaces feel interactive because of fast feedback—not because JavaScript exists.

```css
.button {
    transition:
        transform 80ms ease,
        background 120ms ease,
        box-shadow 120ms ease;
}

.button:hover {
    background: var(--hover);
}

.button:active {
    transform: scale(.98);
}

.button:focus-visible {
    outline: 2px solid var(--focus);
    outline-offset: 2px;
}
```

Cards:

```css
.card {
    transition:
        border-color 120ms ease,
        background 120ms ease,
        transform 120ms ease;
}

.card:hover {
    transform: translateY(-1px);
}
```

Respect reduced motion:

```css
@media (prefers-reduced-motion: reduce) {
    *,
    *::before,
    *::after {
        scroll-behavior: auto !important;
        transition-duration: .001ms !important;
        animation-duration: .001ms !important;
        animation-iteration-count: 1 !important;
    }
}
```

---

## 13. Progressive enhancement tiers

### Tier A — functionality

Safe place for core behavior when supported by the declared browser baseline:

- semantic links/buttons/forms
- `<details>` / `<summary>`
- native form controls
- native form validation
- `:checked`
- `:target`
- `:focus-visible`
- `:focus-within`
- `:has()` where baseline permits
- Grid / Flexbox
- media queries
- custom properties
- ordinary transitions
- Popover where baseline permits

### Tier B — polish

Can disappear without breaking tasks:

- `@starting-style`
- discrete transitions
- intrinsic-size animation helpers
- decorative motion

### Tier C — experimental enhancement

Never the sole path to functionality for conservative browser targets:

- CSS Anchor Positioning
- scroll-driven animations
- newest dialog command invokers
- cross-document View Transitions
- customizable select features

---

## 14. Anti-patterns

### Checkbox as everything

Do not use a hidden checkbox to emulate every menu/modal/tab just because `:checked` exists.

Good:

```html
<input type="checkbox" name="notifications">
```

Bad architectural instinct:

```text
fake modal -> hidden checkbox
fake dropdown -> hidden checkbox
fake route state -> hidden checkbox
fake accordion -> hidden checkbox
```

Use the semantic native primitive instead.

### CSS as a programming-language stunt

If a pattern requires unreadable selector machinery to imitate state the browser/server already owns, it is probably the wrong abstraction.

### Animation-dependent behavior

The UI must not require a transition finishing correctly to enter a usable state.

### New-feature lock-in

A new CSS feature should improve the UI. Unsupported browsers should lose refinement, not access to the feature.

---

## 15. Component design checklist

Before implementing a component, ask:

1. Is there a semantic HTML element for this interaction?
2. Does that element already expose usable browser state?
3. Can CSS react through `:open`, `:checked`, `:target`, `:popover-open`, focus state, or `:has()`?
4. Is this state actually durable application state that belongs in the URL/server instead?
5. Does the keyboard interaction remain correct without JavaScript?
6. Does unsupported CSS remove only polish?
7. Does reduced-motion mode remain usable?
8. Can the server remain authoritative after a full reload?

If the answers are good, the component is a good PureDesign candidate.
