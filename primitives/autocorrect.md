# `autocorrect`

**Role:** let the browser/underlying OS own text autocorrection behavior.

```html
<textarea name="message" autocorrect="on"></textarea>

<input name="username" autocorrect="off">
```

The exact substitutions are user-agent/device behavior; the application does not need to implement a spelling/punctuation replacement engine merely to get ordinary input autocorrection.

## Compatibility

Firefox shipped the `autocorrect` global attribute in **Firefox 136**, so it exists in the Firefox 140 ESR engine baseline.

MDN marks the feature Baseline 2026 across current mainstream browsers, so older engines still need graceful ignore behavior.

## Boundary

Typing assistance -> browser / OS.

Stored/submitted text -> actual form value and server.

Do not assume autocorrect is deterministic across devices.

Email, URL and password input types do not use normal autocorrection behavior.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes/autocorrect
- https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/136
