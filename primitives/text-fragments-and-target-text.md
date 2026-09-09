# Text Fragments and `::target-text`

**Role:** deep-link to exact text and let the browser scroll/highlight the matched passage without client-side JavaScript.

A text fragment lives in the URL fragment directive:

```text
/article#:~:text=browser-owned%20state
```

Supporting browsers locate the matching text, scroll it into view and highlight it. The page can style the matched range:

```css
::target-text {
  background: Highlight;
  color: HighlightText;
}
```

## Why it matters

For documentation, evidence pages, issue summaries and long server-rendered records, this can replace custom "scroll to quote and flash it" JavaScript.

The normal document URL remains the fallback. A browser that ignores the text directive still loads the page.

## Stability boundary

Text fragments match rendered text, not a durable application identifier. Copy edits can break the exact match.

For durable app navigation, prefer a real element `id` and ordinary fragment. Use text fragments when the desired target is a passage rather than an owned structural anchor.

## Privacy boundary

The selected phrase is encoded into the URL. URLs can appear in copied links, browser history, logs or other surfaces. Do not generate text-fragment URLs containing secrets or sensitive user content.

## Compatibility

`::target-text` landed in Firefox 131, so it predates the repository's Firefox 140 ESR engine baseline. Tor Browser may still change or disable web-platform behavior for privacy/security reasons; verify the actual Tor release before making text-fragment behavior important to a task.

## Sources

- MDN Text fragments: https://developer.mozilla.org/en-US/docs/Web/URI/Reference/Fragment/Text_fragments
- MDN `::target-text`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Selectors/::target-text
- CSS Pseudo-Elements Level 4: https://drafts.csswg.org/css-pseudo-4/#selectordef-target-text
