# At-Rule Feature Detection with `at-rule()`

**Role:** test support for a CSS at-rule from `@supports` without JavaScript feature detection or user-agent sniffing.

CSS Conditional Rules Level 5 adds the `at-rule()` support query function:

```css
@supports at-rule(@starting-style) {
  /* Enhancement that assumes @starting-style is recognized. */
}
```

The condition is true when the browser recognizes the named at-rule.

## Why this exists

Traditional `@supports` declaration tests answer questions such as:

```css
@supports (field-sizing: content) { ... }
```

and `selector()` can test selector syntax. Those mechanisms do not directly answer whether an arbitrary at-rule is recognized.

`at-rule()` fills that gap:

```text
CSS property/value -> @supports (property: value)
selector syntax    -> @supports selector(...)
at-rule support    -> @supports at-rule(@...)
```

Useful progressive checks can include newer at-rules such as `@starting-style`, `@property`, `@scope`, `@position-try`, or other future syntax where merely letting an unknown rule be ignored is not enough for the surrounding composition.

## Do not overuse it

CSS already has robust error handling. If an unsupported at-rule can simply disappear while a complete baseline remains, a support query may add needless complexity.

Use `at-rule()` when the surrounding declarations or fallback choice genuinely need to know whether the at-rule exists.

A successful `at-rule()` result also does **not** prove that every descriptor, nested construct, or behavior you intend to use inside that at-rule is supported. Test narrower dependent syntax separately where necessary.

## Architecture boundary

This is capability detection for presentation, not environment detection for application policy.

Do not use feature support as a proxy for:

- user identity;
- permissions;
- device trust;
- security policy;
- browser brand/version business logic.

Prefer capability queries over UA sniffing when CSS capability is the actual question.

## Compatibility

This is **not** core for Firefox 140 ESR / Tor Browser.

As of the 2026-09 snapshot:

- Chromium / Edge 148+ support `at-rule()` in `@supports`;
- WebKit implemented it on main in August 2026, but stable Safari support is not yet a conservative baseline;
- Firefox does not provide support suitable for the repository's conservative target.

Keep a complete baseline outside the query.

## Sources

- https://drafts.csswg.org/css-conditional-5/#at-rule-support
- https://developer.chrome.com/release-notes/148
- https://bugs.webkit.org/show_bug.cgi?id=235400
