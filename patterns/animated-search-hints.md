# CSS-Only Animated Search Hints

Use this pattern when a search field should cycle through example prompts or categories while remaining fully usable with **zero client-side JavaScript**.

The visible rotating text is not the input's real placeholder. It is a presentation layer positioned over the empty input. The browser exposes the empty/placeholder state through `:placeholder-shown`, and CSS animation moves a stack of hint rows through a one-line clipping window.

## Compose

- [native search input and landmark](../primitives/search-input-and-landmark.md)
- [`:placeholder-shown`](../primitives/placeholder-shown.md)
- [`prefers-reduced-motion`](../primitives/prefers-reduced-motion.md)
- [semantic HTML first](../principles/semantic-html-first.md)

## Markup

```html
<search class="header-search">
  <form action="/search" method="get">
    <label class="visually-hidden" for="header-search-q">Search</label>

    <div class="header-search-field">
      <input
        id="header-search-q"
        class="header-search-input"
        type="search"
        name="q"
        value="{{ query }}"
        placeholder=" "
        maxlength="200"
        autocomplete="off"
        spellcheck="false"
      >

      <div class="header-search-hints" aria-hidden="true">
        <div class="header-search-hints-track">
          <!-- duplicate of the last visible state for a seamless loop -->
          <span>Search files</span>
          <span>Search people</span>
          <span>Search folders</span>
          <span>Search posts</span>
          <span>Search files</span>
        </div>
      </div>
    </div>

    <button class="visually-hidden" type="submit">Search</button>
  </form>
</search>
```

`placeholder=" "` is intentional. The single space gives the input a placeholder state without displaying user-facing placeholder copy. The visible hints live in normal HTML next to the input instead.

Keep a real `<label>` even when the product visually hides it. The animated hints are decorative examples, not the accessible name of the control.

## CSS

```css
.visually-hidden {
  position: absolute;
  width: 1px;
  height: 1px;
  padding: 0;
  margin: -1px;
  overflow: hidden;
  clip: rect(0 0 0 0);
  white-space: nowrap;
  border: 0;
}

.header-search-field {
  --hint-line-height: 1.25rem;

  position: relative;
}

.header-search-input {
  position: relative;
  z-index: 2;

  width: 100%;
  min-height: 2.75rem;
  padding-inline: 0.875rem;

  background: transparent;
}

.header-search-input::placeholder {
  color: transparent;
}

.header-search-hints {
  position: absolute;
  z-index: 1;

  inset-inline-start: 0.875rem;
  top: 50%;

  height: var(--hint-line-height);
  overflow: hidden;
  transform: translateY(-50%);

  pointer-events: none;
  color: currentColor;
  opacity: 0.6;
}

.header-search-hints-track {
  display: grid;
  grid-auto-rows: var(--hint-line-height);

  animation: header-search-hints 12s ease-in-out infinite;
}

.header-search-hints-track > span {
  display: flex;
  align-items: center;

  height: var(--hint-line-height);
  line-height: var(--hint-line-height);
  white-space: nowrap;
}

/*
 * The track moves downward.
 * New text enters from the top and the old text exits at the bottom.
 * The first and last rows contain the same text, so the iteration reset
 * is visually invisible.
 */
@keyframes header-search-hints {
  0%,
  16% {
    transform: translateY(calc(var(--hint-line-height) * -4));
  }

  20%,
  36% {
    transform: translateY(calc(var(--hint-line-height) * -3));
  }

  40%,
  56% {
    transform: translateY(calc(var(--hint-line-height) * -2));
  }

  60%,
  76% {
    transform: translateY(calc(var(--hint-line-height) * -1));
  }

  80%,
  100% {
    transform: translateY(0);
  }
}

/* A real value replaces the decorative hint layer automatically. */
.header-search-input:not(:placeholder-shown) + .header-search-hints {
  visibility: hidden;
  opacity: 0;
}

@media (prefers-reduced-motion: reduce) {
  .header-search-hints-track {
    animation: none;
    transform: translateY(calc(var(--hint-line-height) * -4));
  }
}
```

## How it works

```text
input placeholder=" "
        |
        v
:placeholder-shown exposes whether the input is empty
        |
        v
absolute decorative hint viewport
        |
        v
overflow: hidden shows exactly one row
        |
        v
@keyframes + translateY moves the row stack
        |
        v
user types -> :placeholder-shown stops matching -> hints disappear
```

No input event listener, timer, DOM mutation, class toggling or hydration is involved.

## State ownership

```text
query text                  -> native input
empty/non-empty presentation -> :placeholder-shown
hint motion                 -> CSS animation timeline
search request              -> normal GET form submission
search results              -> server-rendered response
reduced-motion preference   -> browser/OS media preference
```

The hints are presentation only. They must not represent application state, selected filters, permissions, validation results or any information required to complete the search.

## Accessibility

- Keep a real `<label>` or another valid accessible name for the search input.
- Mark the rotating hint layer `aria-hidden="true"` so assistive technology does not repeatedly encounter decorative changing text.
- Use `pointer-events: none` on the overlay so it cannot block pointer access to the real input.
- Keep normal form submission available. The pattern must not imply live-search behavior that does not exist.
- Respect `prefers-reduced-motion: reduce`; a static hint is sufficient.
- Do not place critical instructions only inside the animation.

## Server-rendered values

When the server renders a non-empty query back into the input:

```html
<input name="q" value="report" placeholder=" ">
```

`:placeholder-shown` does not match, so the decorative hints stay hidden without any browser-side state synchronization.

When the value is empty, the hints return automatically.

## Variants

To make the stack move upward instead, place the duplicate row at the end and animate from `translateY(0)` toward progressively more-negative offsets. Keep the duplicate endpoint so the iteration reset remains invisible.

The hint phrases may be rendered by the server. Do not use CSS generated `content` as the only source of meaningful text; explicit markup is easier to reason about and keeps presentation separate from semantics.

## Compatibility

This pattern intentionally depends on long-established HTML/CSS behavior rather than experimental selectors or browser APIs. The search action itself remains a normal form submission even if animation styling is unavailable.

Test the final product with scripting disabled and with reduced motion enabled. Also test autofill and server-rendered non-empty values because both can expose mistakes in empty-state styling.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/:placeholder-shown
- https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_animations/Using_CSS_animations
- https://developer.mozilla.org/en-US/docs/Web/CSS/transform
- https://developer.mozilla.org/en-US/docs/Web/CSS/pointer-events
- https://developer.mozilla.org/en-US/docs/Web/CSS/@media/prefers-reduced-motion
