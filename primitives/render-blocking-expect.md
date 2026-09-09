# Render Blocking with `rel="expect"`

**Role:** let a server-rendered document delay its first render until a specific later DOM node has been parsed, without a client-side readiness script.

```html
<head>
  <link rel="expect" href="#lead-content" blocking="render">
</head>
<body>
  <header>...</header>
  <main id="lead-content">...</main>
</body>
```

The `href` points to an element ID in the same document. With `blocking="render"`, the browser can hold rendering until that node has been parsed.

## Useful composition

This is particularly relevant to [cross-document View Transitions](view-transitions.md). A server-rendered destination page can make sure the HTML required for its initial transition state exists before the browser paints the new document.

It can also reduce an inconsistent first paint when the critical visible subtree appears later in the streamed/parser order.

## This is not

```text
rel=expect != fetch data
rel=expect != wait for an API
rel=expect != client state
rel=expect != general loading screen primitive
```

It waits for parser progress to the referenced DOM node. It does not replace server work or resource loading architecture.

## Performance rule

Render blocking delays visible output. Reference the smallest genuinely critical boundary and measure the result. Do not hold the whole page for below-the-fold content merely to make a transition prettier.

Keep normal document navigation and usable HTML as the baseline. Losing this feature must remove only paint/transition polish.

## Compatibility

This is **not** core for Firefox 140 ESR / Tor Browser.

Current support is Chromium-led; Firefox and Safari do not provide a conservative interoperable baseline for it in the 2026-09 snapshot. Treat it as progressive enhancement and re-check the compatibility matrix before relying on it.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/rel#expect
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/link
- https://developer.mozilla.org/en-US/docs/Web/API/View_Transition_API/Using
- https://web.dev/blog/interop-2026

## Research examples

- https://github.com/nearestnabors/alice-in-videoland
- https://github.com/cydstumpel/view-transitions
