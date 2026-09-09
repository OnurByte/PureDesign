# Real Anchor Navigation

**Role:** preserve browser navigation semantics instead of implementing links as click-driven JavaScript.

```html
<a href="/files/42">Open file</a>
```

A real `<a href>` gives the browser ownership of navigation behavior, including user-controlled new-tab/window behavior, copying/dragging the link, bookmarking, keyboard activation and normal history/navigation semantics.

## Do not

```html
<a href="#" onclick="openFile()">Open file</a>
```

or:

```html
<div role="link" tabindex="0">Open file</div>
```

for ordinary navigation.

If the action changes the current document or application URL, use a real link. If it performs an in-place action, use a real button/form control.

## Why this matters for zero-JS

Fake links fail especially badly while JavaScript is loading, errors, or is disabled. They also break expected browser affordances such as copy-link and open-in-new-tab.

## Compose

- [`aria-current`](aria-current.md) for the server-known current link.
- [`target`](target.md) for fragment navigation.
- [`scroll-behavior`](scroll-behavior.md) and [`scroll-offsets`](scroll-offsets.md) for optional fragment polish.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/a
- https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Accessibility/HTML
