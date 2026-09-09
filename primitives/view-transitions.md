# Cross-Document View Transitions

**Role:** optional MPA navigation polish without requiring a client-side SPA runtime.

A same-origin multi-page application can opt into navigation transitions with CSS in supporting browsers:

```css
@view-transition {
  navigation: auto;
}
```

The important point is architectural: server-rendered navigation can gain SPA-like visual continuity without moving routing/state to the client.

## Stabilizing destination markup

When a transition needs critical destination markup to have been parsed before the first render, supporting browsers can combine this with [`rel="expect"` render blocking](render-blocking-expect.md):

```html
<head>
  <link rel="expect" href="#lead-content" blocking="render">
</head>
```

This is progressive paint/transition polish, not a new navigation model. The destination remains a normal server-rendered document.

## Rule

Navigation must remain ordinary document navigation. If view transitions or `rel="expect"` are unsupported, the page should simply navigate normally.

Do not delay rendering for non-critical content merely to make an animation prettier.

## Compatibility

Do not treat cross-document view transitions or `rel="expect"` render blocking as core behavior for Firefox 140 ESR / Tor Browser targets.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/API/View_Transition_API/Using
- https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/147
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/rel#expect
