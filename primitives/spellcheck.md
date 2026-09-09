# `spellcheck`

**Role:** opt editable text into or out of browser-provided spellchecking without bundling a spelling UI/runtime.

```html
<textarea name="article" spellcheck="true"></textarea>

<textarea name="secret_note" spellcheck="false"></textarea>
```

## Privacy boundary

Spellchecking is not guaranteed to be local.

The HTML specification does not dictate how a browser implements spellcheck, and MDN warns that editable content **may be sent to a third party** by browser configurations that use enhanced spellchecking services.

For sensitive/private fields, explicitly consider:

```html
spellcheck="false"
```

Examples may include:

- secrets or recovery material
- private notes
- encrypted-message plaintext before submission
- sensitive search/query fields

## Rules

- `spellcheck` is a user-agent capability, not application validation.
- Never rely on it to enforce spelling/content policy.
- Do not enable it globally without considering data sensitivity.
- A privacy-first product may intentionally disable it for more fields than a general-purpose site.

## Source

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes/spellcheck
