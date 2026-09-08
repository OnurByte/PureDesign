# Cross-Document View Transitions

**Role:** optional MPA navigation polish without requiring a client-side SPA runtime.

A same-origin multi-page application can opt into navigation transitions with CSS in supporting browsers:

```css
@view-transition {
  navigation: auto;
}
```

The important point is architectural: server-rendered navigation can gain SPA-like visual continuity without moving routing/state to the client.

## Rule

Navigation must remain ordinary document navigation. If view transitions are unsupported, the page should simply navigate normally.

## Compatibility

Do not treat cross-document view transitions as core behavior for Firefox 140 ESR / Tor Browser targets.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/API/View_Transition_API/Using
- https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/147
