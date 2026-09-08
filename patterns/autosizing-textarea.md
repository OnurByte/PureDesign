# Autosizing textarea

## Goal

Provide a native message/comment composer that grows with entered text without client-side JavaScript.

## Baseline

Always start with a usable `<textarea>`:

```html
<label for="message">Message</label>
<textarea id="message" name="message" rows="4" maxlength="4000"></textarea>
```

## Progressive enhancement

```css
textarea {
    inline-size: 100%;
    min-block-size: 3lh;
    max-block-size: 14lh;
}

@supports (field-sizing: content) {
    textarea {
        field-sizing: content;
        overflow-y: auto;
    }
}
```

The maximum size matters: a composer that grows to consume the entire viewport is not an improvement.

## Ownership

```text
text value        -> native textarea/form
intrinsic sizing  -> browser via field-sizing
validation        -> native constraints + server
submission        -> form/HTTP/server
```

No `input` listener and no `scrollHeight` measurement are needed in supporting browsers.

## Tor / ESR

Firefox 140 ESR does not have `field-sizing`; Firefox added it in 152. Therefore Tor Browser 15 gets the normal fixed/bounded textarea fallback.

## Read

- [`../primitives/field-sizing-content.md`](../primitives/field-sizing-content.md)
- [`../primitives/native-validation.md`](../primitives/native-validation.md)
- [`../compatibility/tor-browser-firefox-esr.md`](../compatibility/tor-browser-firefox-esr.md)
