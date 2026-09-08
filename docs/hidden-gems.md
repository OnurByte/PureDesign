# Hidden Gems: Small No-JS UI Sources Worth Studying

This is the research notebook behind PureDesign.

The goal is not to collect the most popular CSS frameworks. It is to preserve **small repositories, gists, discussions, and Reddit threads that contain unusually useful implementation ideas**.

> Visibility numbers below are snapshots/approximations observed during research on **2026-09-08**. Stars, votes, and comments can change.

---

## 1. YieldRay — `css-only-demo.html`

**Source:** https://gist.github.com/YieldRay/3d965bf568332a25c38f8c00fb79285e  
**Observed visibility:** essentially undiscovered; 0-star gist during research.

### Why it matters

This single-file demo combines several modern platform primitives that are usually discussed separately:

- Popover API
- Declarative Shadow DOM
- `:has()`-driven theme state
- `<details>` animation
- intrinsic-size animation helpers
- discrete transitions

The interesting part is not the visual demo itself. It is the architecture.

### Pattern: Declarative Shadow DOM without JavaScript

```html
<example-menu>
    <template shadowrootmode="open">
        <style>
            menu[popover] {
                /* isolated component styles */
            }
        </style>

        <menu popover>
            ...
        </menu>
    </template>
</example-menu>
```

Traditional Shadow DOM examples usually begin with JavaScript:

```js
element.attachShadow({ mode: "open" })
```

Declarative Shadow DOM lets server-rendered HTML establish that boundary directly.

### Pattern: theme state with real form controls

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

### What to steal

- the state ownership model
- the combination of HTML-native primitives
- the idea that server-rendered components can still have strong style isolation

### What not to assume

Declarative Shadow DOM should not be introduced everywhere. Shadow boundaries affect styling, composition, forms, and accessibility. Use it only where isolation earns its complexity.

---

## 2. blackspike — `popover-menu.css`

**Source:** https://gist.github.com/blackspike  
**Observed visibility:** 0-star gist during research.

### Why it matters

It demonstrates a modern floating-menu stack:

```text
invoker
   |
   v
popover
   |
   +-- top layer
   |
   +-- CSS anchor positioning
```

A representative shape is:

```css
.nav-mobile-toggler {
    anchor-name: --nav-toggler;
}

.nav-mobile {
    position-anchor: --nav-toggler;
    position-area: block-end span-inline-start;
}
```

This replaces a class of JavaScript that often looks like:

```text
getBoundingClientRect()
calculate X/Y
watch resize
watch scroll
move overlay
```

### What to steal

The idea that floating UI is becoming a browser-layout problem rather than necessarily a JavaScript positioning problem.

### What not to do

Do not make CSS Anchor Positioning the only path for conservative/ESR browser targets. Keep a conventional positioning fallback.

---

## 3. viliket — `pure-web-bottom-sheet`

**Repository:** https://github.com/viliket/pure-web-bottom-sheet  
**Observed visibility:** ~64 GitHub stars during research.  
**Related Reddit thread:** https://www.reddit.com/r/css/comments/1on7rhn/

### Why it matters

This is one of the strongest conceptual findings in the research.

Instead of implementing a mobile bottom sheet through pointer tracking and transforms, model it as a **scrolling system**.

Typical JavaScript approach:

```text
pointerdown
pointermove
velocity calculation
requestAnimationFrame
translateY
snap threshold
pointerup
```

Alternative model:

```css
.bottom-sheet {
    overflow-y: auto;
    scroll-snap-type: y mandatory;
}

.bottom-sheet__snap {
    scroll-snap-align: start;
}
```

Now browser scrolling owns momentum and snapping.

### The deeper lesson

Do not ask:

> How do I reproduce this JavaScript interaction in CSS?

Ask:

> Which native browser primitive already has the same physics or state model?

This gives a useful mapping:

```text
bottom sheet -> scrolling
carousel     -> horizontal scrolling
dropdown     -> popover
accordion    -> disclosure
modal        -> dialog
```

### What to steal

The abstraction, even if you never use the repository itself.

---

## 4. Johannes Mutter — AnchorPop

**Repository:** https://github.com/johannesmutter/anchorpop  
**Observed visibility:** ~33 GitHub stars during research.

### Why it matters

AnchorPop is packaged for Svelte, but the interesting part is below the framework layer.

It explores:

- CSS Anchor Positioning
- `@position-try` fallbacks
- anchored container-query ideas
- arrow positioning
- top-layer interaction
- a “Trigger Proxy Pattern” for difficult positioning relationships

### Mental model

A JavaScript floating-positioning library often does:

```text
computePosition()
  -> flip()
  -> shift()
  -> offset()
```

Modern CSS can increasingly express:

```text
preferred position
      |
      v
position try fallback
      |
      v
alternate position
```

### What to steal

Read the CSS, not the Svelte API.

The repository is useful as a laboratory for what can move from Popper/Floating-UI-style JavaScript into CSS.

### What not to assume

Support is still browser-version-sensitive. Treat this as enhancement unless your browser matrix explicitly guarantees it.

---

## 5. TeamDijon — `details-animation-support.css`

**Source:** https://gist.github.com/TeamDijon  
**Observed visibility:** 0-star gist during research.

### Why it matters

The value is not just animated `<details>`; it is the fallback structure.

Representative architecture:

```css
@media (prefers-reduced-motion: no-preference) {
    details {
        transition: .3s ease-in-out;
    }

    @supports (interpolate-size: allow-keywords) {
        details {
            interpolate-size: allow-keywords;
        }

        details::details-content {
            block-size: 0;
            opacity: 0;
        }
    }
}
```

This produces the correct hierarchy:

```text
feature supported
    -> polished animation

feature unsupported
    -> normal details behavior

reduced motion requested
    -> little/no animation
```

### What to steal

**Progressive enhancement structure.**

Functionality should not live inside `@supports`.

---

## 6. webfactory — `dialog-utils`

**Repository:** https://github.com/webfactory/dialog-utils  
**Observed visibility:** ~3 stars during research.

### Why it matters

This repository uses JavaScript for progressive enhancement/polyfilling, so it is **not** itself a zero-JS dependency recommendation.

Its value is different: it is a window into the direction of declarative dialog APIs.

Example shape:

```html
<button commandfor="my-dialog" command="show-modal">
    Open
</button>

<dialog id="my-dialog">
    <button commandfor="my-dialog" command="close">
        Close
    </button>
</dialog>
```

Related modern concepts include declarative close/light-dismiss behavior such as `closedby`.

### What to steal

Watch which imperative JavaScript APIs are becoming declarative HTML attributes.

### What not to steal

Do not add the polyfill if your product contract is truly zero client-side JavaScript. Use the repository as research.

---

## 7. Demetris — Omni Carousel

**Repository:** https://github.com/demetris/omni-carousel  
**Observed visibility:** ~8 stars during research.  
**Related Reddit:** https://www.reddit.com/r/webdev/comments/1ofl0f3/

### Why it matters

Omni Carousel contains JavaScript, so again it is not a PureDesign dependency.

The useful lesson is architectural: **the base carousel can remain a normal scrollable document.**

```css
.track {
    display: flex;
    overflow-x: auto;
    scroll-snap-type: x mandatory;
}

.slide {
    scroll-snap-align: start;
}
```

Optional JavaScript can add convenience, but the content is not held hostage by a runtime.

### What to steal

This progression:

```text
HTML -> usable
CSS  -> pleasant
JS   -> optional convenience
```

instead of:

```text
JS runtime -> interface exists
runtime fails -> interface disappears
```

---

## 8. Digicreon — µCSS

**Repository:** https://github.com/Digicreon/muCSS  
**Observed visibility:** roughly 109 GitHub stars; related Reddit post received little attention during research.  
**Reddit:** https://www.reddit.com/r/css/comments/1rqu09n/

### Why it matters

µCSS demonstrates that a fairly broad component vocabulary can still be implemented in CSS-first form:

- accordion
- modal
- navigation
- tabs
- toast
- pagination
- progress
- skeletons
- spinners
- forms
- cards

### What to steal

Do not necessarily import the framework. Inspect individual component styles to see where semantic HTML is enough.

Useful files to study conceptually:

```text
modal
tabs
nav
toast
```

Small frameworks often have less historical compatibility baggage than Bootstrap-class projects, making their component logic easier to inspect.

---

## 9. Pico CSS — Discussion #343

**Discussion:** https://github.com/picocss/pico/discussions/343

### Why it matters

The useful material is hidden in a GitHub Discussion rather than in a repository README.

A no-JS responsive navigation can use a disclosure:

```html
<details>
    <summary>☰</summary>
    <nav>
        ...
    </nav>
</details>
```

More modern browsers can move toward declarative dialog invocation:

```html
<button command="show-modal" commandfor="dialog-navigation">
    ☰
</button>

<dialog id="dialog-navigation">
    ...
</dialog>
```

### What to steal

The decision hierarchy:

```text
semantic browser primitive
        ^
        |
checkbox hack only when state is actually checkbox-like
```

Do not choose a hidden checkbox just because `:checked` is convenient.

---

## 10. Low-visibility Reddit `<details>` discussions

### Animated FAQ / `<details name>`

**Thread:** https://www.reddit.com/r/css/comments/1vwv16h/

The implementation explores modern `<details>` animation and grouped disclosures.

The more important finding is an edge case mentioned in discussion: auto-closing one long disclosure while opening another can cause unpleasant scroll movement on mobile.

### Another small `<details>` animation thread

**Thread:** https://www.reddit.com/r/css/comments/1g4d2aa/

This explores `<details>` animation with newer CSS techniques while preserving semantic markup.

### Lesson

Community comments often reveal the thing demos omit:

> A primitive can be technically native and still need UX testing.

---

## 11. Low-visibility Reddit `:user-invalid` discussion

**Thread:** https://www.reddit.com/r/css/comments/1oasqw0/

### Why it matters

A common form style is:

```css
input:invalid {
    border-color: red;
}
```

But a required field can be invalid before a user meaningfully interacts with it.

A better UI signal in many cases is:

```css
input:user-invalid {
    border-color: var(--danger);
}
```

Combined with `:has()`:

```css
.field:has(input:user-invalid) {
    border-color: var(--danger);
}
```

### Deeper lesson

Focus is not necessarily intent to edit. A keyboard or assistive-technology user may focus controls while exploring the page.

Validation styling should distinguish **invalid data** from **user-caused validation feedback**.

---

## 12. Adam Bien — `unscripted`

**Repository:** https://github.com/AdamBien/unscripted

This is more visible than the sources above, but it is valuable enough to keep as an index.

Its theme is essentially the same research question as PureDesign: which SPA-era JavaScript responsibilities now have browser-native equivalents?

Topics include:

- popovers
- dialogs
- details
- form validation
- view transitions
- CSS carousel patterns
- anchor positioning
- container queries
- scroll animations

### What to steal

Use it as a feature map, then validate each feature against your actual browser baseline before depending on it.

---

## 13. MinimaCSS / Frutjam / Pico CSS

These are broader references from the first research pass.

### MinimaCSS

https://github.com/hardikforall/MinimaCSS

Interesting for native popover/modal/accordion patterns and modern transition primitives such as `@starting-style` and discrete transitions.

### Frutjam

https://github.com/nezanuha/frutjam

Its implementation stack may not match a plain-CSS project, but its component catalog is useful for seeing how much UI can be expressed through `<dialog>`, `popover`, `<details>`, and `:has()`.

### Pico CSS

https://github.com/picocss/pico

Useful primarily as a semantic-HTML styling reference. It demonstrates how much UI quality can come from styling native structure rather than replacing it.

### Classless CSS collection

https://github.com/dbohdan/classless-css

Useful as a visual/reference catalog of projects that make plain semantic HTML look deliberate with very little markup ceremony.

---

# Research conclusions

The best findings were not “clever CSS tricks.” They repeatedly pointed toward the same architecture.

## Browser state

```text
:checked
:open / [open]
:popover-open
:focus-visible
:focus-within
:user-invalid
:target
        |
        v
      :has()
        |
        v
       CSS
```

## Durable state

```text
link / form
    |
    v
   HTTP
    |
    v
 server
    |
    v
 rendered HTML
```

## Best conceptual discoveries

1. **Bottom sheets as scrolling systems** — stop reproducing browser physics manually.
2. **Popover + Anchor Positioning** — floating UI is moving into declarative layout.
3. **Declarative Shadow DOM** — server-rendered component isolation does not inherently require JavaScript.
4. **Native validation + `:has()`** — much visual form state does not require class toggling.
5. **`<details>` fallback architecture** — functionality outside `@supports`, polish inside it.
6. **URL as state** — browser history, bookmarks, reloads, and deep links become features instead of synchronization problems.

# How to evaluate future findings

A small repository is worth adding here only if it contributes at least one of these:

- a better semantic primitive
- a simpler state model
- a robust fallback
- a useful browser-native physics mapping
- a real accessibility insight
- a technique that removes a JavaScript dependency without making the CSS absurd

Low star count alone is not a quality signal.
