# `autocapitalize`

**Role:** hint capitalization behavior to virtual keyboards and voice-input systems without device-detection JavaScript.

```html
<input
  name="display_name"
  autocapitalize="words">

<textarea
  name="message"
  autocapitalize="sentences"></textarea>
```

Common values include:

- `none`
- `sentences`
- `words`
- `characters`

## What this replaces

Not text transformation after submission. It replaces UI code that detects mobile/input method and attempts to configure or imitate keyboard capitalization behavior.

## Boundary

Input-method suggestion -> browser / OS.

Canonical stored value -> server/application validation.

Do not use CSS/JS capitalization as a substitute: `text-transform` changes presentation, not the submitted value.

## Compatibility

MDN currently marks `autocapitalize` as Limited Availability across the full browser landscape. Treat it as a harmless input hint: unsupported browsers simply ignore it.

## Source

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes/autocapitalize
