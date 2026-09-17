# Recovery Phrase Save-and-Confirm Screen

A recovery phrase screen can feel application-like without clipboard scripts, DOM state or a frontend runtime. Let the browser own form validity and selection, let CSS render that state, and keep download/recovery authority on the server.

## Goal

Build a screen that:

- shows a numbered 12-word phrase in a compact responsive grid;
- makes the whole phrase easy to select manually;
- places a download action inside the phrase card without covering text;
- requires the user to acknowledge that the phrase was saved;
- visually strengthens the Continue action after acknowledgement;
- remains usable with client-side JavaScript disabled;
- can fill the mobile viewport without the classic `window.innerHeight` workaround.

## Markup

```html
<main class="recovery-shell">
  <form class="recovery-form" action="/register/confirm-recovery" method="post">
    <header>
      <h1>Recovery phrase</h1>
      <p>Write down these 12 words in order. You will need them to recover your account.</p>
    </header>

    <aside class="warning" role="note">
      Store this phrase securely. It will not be shown again.
    </aside>

    <div class="phrase-wrap">
      <ol class="phrase-grid">
        <li><span class="phrase-index">1.</span> aisle</li>
        <li><span class="phrase-index">2.</span> size</li>
        <li><span class="phrase-index">3.</span> trim</li>
        <li><span class="phrase-index">4.</span> bird</li>
        <li><span class="phrase-index">5.</span> device</li>
        <li><span class="phrase-index">6.</span> disagree</li>
        <li><span class="phrase-index">7.</span> scare</li>
        <li><span class="phrase-index">8.</span> left</li>
        <li><span class="phrase-index">9.</span> tourist</li>
        <li><span class="phrase-index">10.</span> travel</li>
        <li><span class="phrase-index">11.</span> depart</li>
        <li><span class="phrase-index">12.</span> belt</li>
      </ol>

      <div class="phrase-actions">
        <a class="icon-action"
           href="/register/recovery-phrase/download"
           download
           aria-label="Download recovery phrase">
          ↓
        </a>
      </div>
    </div>

    <label class="saved-check">
      <input type="checkbox" name="phrase_saved" value="1" required>
      <span>I have saved my recovery phrase</span>
    </label>

    <button class="continue" type="submit">Continue</button>
  </form>
</main>
```

Use the server/framework's normal CSRF mechanism in real applications; it is omitted above only to keep the example framework-neutral.

## CSS

```css
.recovery-shell {
  min-block-size: 100svh;
  display: grid;
  place-items: center;
  padding: 1.5rem;
}

.recovery-form {
  inline-size: min(100%, 32rem);
  display: grid;
  gap: 1.25rem;
}

.phrase-wrap {
  position: relative;
}

.phrase-grid {
  margin: 0;
  padding: 1rem 3.5rem 1rem 1rem;
  list-style: none;
  display: grid;
  grid-template-columns: repeat(2, minmax(0, 1fr));
  gap: .5rem 1.5rem;
  border: 1px solid var(--border);
  border-radius: .75rem;
  background: var(--muted-surface);
  font-family: ui-monospace, monospace;
  user-select: all;
}

.phrase-index {
  display: inline-block;
  inline-size: 2.5ch;
  color: var(--muted-text);
  font-variant-numeric: tabular-nums;
}

.phrase-actions {
  position: absolute;
  inset-block-start: .5rem;
  inset-inline-end: .5rem;
  display: flex;
  gap: .375rem;
}

.icon-action {
  display: inline-grid;
  place-items: center;
  inline-size: 2.25rem;
  block-size: 2.25rem;
  border: 1px solid var(--border);
  border-radius: .5rem;
  text-decoration: none;
}

.continue {
  opacity: .55;
  transition: opacity 120ms ease;
}

.recovery-form:has(input[name="phrase_saved"]:checked) .continue {
  opacity: 1;
}

@media (max-width: 30rem) {
  .phrase-grid {
    grid-template-columns: 1fr;
  }
}
```

The extra inline-end padding on `.phrase-grid` reserves room for the absolutely positioned action so text does not sit underneath it. Logical properties (`inset-inline-end`, `inline-size`, `block-size`) keep the composition friendlier to different writing directions.

## Why the Continue button works without JavaScript

The checkbox is real form state:

```html
<input type="checkbox" name="phrase_saved" required>
```

The browser owns its checked/valid state. `:has()` only observes that state to improve presentation:

```css
.recovery-form:has(input[name="phrase_saved"]:checked) .continue {
  opacity: 1;
}
```

The opacity change is **not** the enforcement mechanism. Native `required` validation prevents an ordinary form submission while the checkbox is unchecked. The server must still validate whatever acknowledgement or onboarding state matters to the application.

Do not use `pointer-events: none` to fake a disabled button. That would hide the browser's useful native validation path and turn presentation into pseudo-authorization.

## Download without JavaScript

For a same-origin endpoint, a real link can request download behavior:

```html
<a href="/register/recovery-phrase/download" download>Download</a>
```

For sensitive one-time material, the server should authorize the request and return an attachment response. If application semantics require POST + CSRF, use a real form submit button and let `Content-Disposition: attachment` drive the download instead of putting secrets into the URL.

See [`../primitives/download-attribute.md`](../primitives/download-attribute.md).

## Manual copy instead of fake clipboard behavior

`user-select: all` makes selection convenient:

```css
.phrase-grid { user-select: all; }
```

It does **not** write to the clipboard. A true one-click Copy button requires clipboard scripting and is therefore outside PureDesign. Keep the phrase visibly selectable and let the user invoke the browser/OS copy command.

See [`../primitives/user-select-all.md`](../primitives/user-select-all.md).

## Numeric alignment

Use tabular numerals for the indexes while still reserving explicit space:

```css
.phrase-index {
  inline-size: 2.5ch;
  font-variant-numeric: tabular-nums;
}
```

See [`../primitives/tabular-numerals.md`](../primitives/tabular-numerals.md).

## Viewport and theme composition

`100svh` gives this auth shell a stable small-viewport minimum without resize listeners. See [`../primitives/dynamic-viewport-units.md`](../primitives/dynamic-viewport-units.md).

If the screen also needs an immediate Light/System/Dark selector, compose it with [`theme-switcher.md`](theme-switcher.md). That pattern already uses real radio state plus `:has()` instead of a JavaScript theme store.

## Responsive visibility

Secondary fixed-position help can be hidden on compact screens with a normal media query, then exposed when enough viewport space exists:

```css
.help-link { display: none; }

@media (min-width: 48rem) {
  .help-link {
    display: block;
    position: fixed;
    inset-inline-end: 1.5rem;
    inset-block-end: 1.5rem;
  }
}
```

This is presentation-only. Do not hide task-critical recovery instructions behind a viewport breakpoint.

## Compose

- [`:has()`](../primitives/has.md)
- [native selection state](../primitives/form-selection-state.md)
- [native form validation](../primitives/native-validation.md)
- [download attribute](../primitives/download-attribute.md)
- [`user-select: all`](../primitives/user-select-all.md)
- [tabular numerals](../primitives/tabular-numerals.md)
- [dynamic viewport units](../primitives/dynamic-viewport-units.md)
- [logical properties](../primitives/logical-properties.md)
- [theme switching](theme-switcher.md)
- [server-authoritative state](../principles/server-authoritative-state.md)

## Security boundary

Recovery phrases are credentials. CSS must never become the trust boundary.

The server owns authentication, CSRF, phrase issuance, confirmation, expiry/revocation rules and download authorization. Do not place the phrase itself in a query string, fragment, analytics event or third-party resource URL.

## Zero-JS test

With scripting disabled, verify that:

1. the complete phrase is visible and selectable;
2. the download route still returns the intended attachment;
3. the required checkbox blocks ordinary submit until checked;
4. the Continue button's visual state follows `:checked`;
5. one-column fallback remains readable on narrow screens;
6. keyboard focus reaches the checkbox, download link and submit button in a sensible order;
7. no essential action depends on a hidden `.js-only` control.
