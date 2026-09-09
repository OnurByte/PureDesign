# Server-Backed Inline Result / Preview Panel

Use a named `<iframe>` as the target of a normal form submission when a bounded server-rendered preview/result should update without navigating the entire parent document.

This is a narrow native browsing-context pattern, not a general SPA replacement.

## Compose

- [named browsing-context targets](../primitives/named-browsing-context-targets.md)
- [native multi-action forms](../primitives/multi-action-forms.md)
- watchlist: [responsive iframe content sizing](../primitives/responsive-iframe-sizing-watchlist.md)

## Example

```html
<form action="/markdown/preview" method="post" target="preview-frame">
  <label for="source">Markdown</label>
  <textarea id="source" name="source" required></textarea>

  <button type="submit">Preview here</button>
  <button type="submit" formtarget="_self">Open preview as page</button>
</form>

<section aria-labelledby="preview-heading">
  <h2 id="preview-heading">Preview</h2>
  <iframe
    class="preview-frame"
    name="preview-frame"
    title="Markdown preview"
    src="/markdown/preview/empty">
  </iframe>
</section>
```

```css
.preview-frame {
  inline-size: 100%;
  block-size: 30rem;
  border: 1px solid;
}
```

Submitting the first button navigates only the named child browsing context. The second button provides ordinary full-page navigation using the same server endpoint.

## Good uses

- server-rendered document/email preview;
- print/PDF preview endpoint;
- bounded query/report result panel;
- rendered markup preview where the server already owns rendering;
- configuration preview whose result does not need to become parent-page state.

## Do not use it for durable parent-page state

The parent page URL does not encode navigation occurring inside the child frame.

If users need to bookmark, share, reload, or deep-link the result as part of the main application state, prefer an ordinary GET route / full-page server render instead.

Do not build an entire application from nested frames merely to avoid navigation.

## Accessibility

- give the iframe a meaningful `title`;
- keep a visible heading around the result region;
- make the embedded response a normal semantic document with its own `<title>`;
- preserve an ordinary full-page route when the framed interaction creates unnecessary navigation complexity;
- do not rely on focus being moved into the new frame automatically after submission.

If confirmation that the preview changed is essential to a task, test the actual assistive-technology workflow rather than assuming the frame navigation is announced sufficiently.

## Security

The preview endpoint is still an application endpoint. Validate and encode all submitted content.

If rendering user-authored HTML, do not inject it unsanitized merely because it is inside an iframe. Decide whether the frame needs a `sandbox`, and grant only the capabilities required by the preview.

The server must apply the same authorization/CSRF rules that would apply if the endpoint were opened as a full page.

## Sizing

Today, use an explicit/minimum block size and allow the child document to scroll.

Future-facing [`frame-sizing`](../primitives/responsive-iframe-sizing-watchlist.md) may remove parent/child height-measurement scripts where supported, but it is not a current conservative dependency.

## Research examples

GitHub contains long-lived real-world uses of form-to-frame previews, including server-rendered sequence diagrams, signature previews and newsletter previews. The useful primitive is the browser target model, not those projects' framework code.

- https://github.com/davidje13/SequenceDiagram
- https://github.com/luksm/PHP-Signature-Generator
- https://github.com/avisota/contao-core
