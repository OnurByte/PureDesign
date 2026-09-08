# `content-visibility: auto`

**Role:** Stable performance primitive. Suitable for progressive use in long server-rendered documents/lists.

`content-visibility: auto` lets the browser skip layout and paint work for off-screen subtrees until they become relevant.

```css
.message,
.file-row,
.feed-item {
    content-visibility: auto;
    contain-intrinsic-size: auto 84px;
}
```

## What the browser owns

For off-screen content, the browser may skip expensive rendering work while keeping the content in the document.

With `auto`, skipped content remains available to:

- Find in Page
- sequential keyboard navigation
- selection/focus
- the accessibility tree

This is a major difference from `content-visibility: hidden` or `display: none`.

## Replaces part of the reason people reach for JS virtualization

For a server-rendered list containing hundreds or thousands of already-present items, this can remove much of the off-screen layout/paint cost without:

- `IntersectionObserver`
- DOM pruning
- mounting/unmounting rows
- client render windows

## It is not true data virtualization

It does **not** reduce:

- response size
- DOM node count
- database work
- transferred data
- memory used by all DOM content

For enormous datasets, paginate on the server first. Then use `content-visibility: auto` to reduce render cost inside each returned page.

## `contain-intrinsic-size`

Give the browser a reasonable placeholder size so the scrollbar and page geometry do not jump while skipped content becomes rendered.

```css
.row {
    content-visibility: auto;
    contain-intrinsic-size: auto 72px;
}
```

The `auto` form lets the browser remember the real size after an item has been rendered.

## Sources

- MDN: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/content-visibility
- MDN auto-state event/accessibility notes: https://developer.mozilla.org/en-US/docs/Web/API/Element/contentvisibilityautostatechange_event
- Small real-world experiment: https://github.com/Arafat481/DOM-Pruner-For-ChatGPT-Gemini
- Vercel agent rule using the same primitive for long lists: https://github.com/vercel-labs/agent-skills/blob/main/skills/react-best-practices/rules/rendering-content-visibility.md
