# Named Browsing-Context Targets

**Role:** send ordinary link or form navigation into a specific existing browsing context, such as a named `<iframe>`, without client-side routing code.

```html
<iframe
  name="preview"
  title="Preview"
  src="/preview/empty">
</iframe>

<form action="/preview" method="get" target="preview">
  <label>
    Markdown
    <textarea name="source"></textarea>
  </label>
  <button type="submit">Preview</button>
</form>
```

The browser resolves `target="preview"` to the browsing context created by `name="preview"` and loads the form response there.

The same targeting model is available to links and can be overridden per submitter with `formtarget`.

## What this replaces

For bounded server-backed panels it can replace a client sequence such as:

```text
preventDefault()
-> serialize form
-> fetch response
-> find panel
-> inject/replace markup
```

The response remains a complete document in its own browsing context. This is **not** DOM fragment replacement.

## State boundary

The parent document URL does not become the authoritative URL for navigation that happens inside the child frame. Do not use a targeted frame when the result must be represented by the parent URL for bookmarking, sharing, reload recovery or ordinary page history semantics.

Provide a normal-navigation route when durable/shareable state matters. A useful composition is a second submit button with `formtarget="_self"`.

## Accessibility

Every iframe needs a concise `title` describing its purpose. The embedded document should have a matching/useful document `<title>` and normal semantic structure.

Do not create many nested browsing contexts to imitate an application window manager. Moving between the parent document and embedded documents can add navigation cost for assistive-technology users.

## Security and privacy

Treat the framed response as a separate document and apply the same output encoding, CSP, authorization and CSRF rules as any other endpoint.

Use `sandbox` only after deciding which capabilities the embedded document actually needs. An overly restrictive sandbox can break forms/navigation; an overly permissive one defeats the isolation you expected.

Same-origin content is usually easier to reason about for an application-owned result panel. Avoid embedding arbitrary user-controlled third-party pages merely to reuse this pattern.

## Compatibility

Named iframe targets, `form[target]`, link `target`, and submitter `formtarget` are mature HTML behavior and may participate in core behavior after product testing on the conservative Firefox/Tor target.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/form#target
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/iframe#name
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/button#formtarget

## Research examples

- https://github.com/davidje13/SequenceDiagram
- https://github.com/luksm/PHP-Signature-Generator
- https://github.com/avisota/contao-core
