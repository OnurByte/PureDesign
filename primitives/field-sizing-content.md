# `field-sizing: content`

**Role:** Progressive enhancement. Not core for Tor Browser 15 / Firefox 140 ESR.

`field-sizing: content` lets native form controls grow or shrink around their contents without measuring `scrollHeight`, listening for `input`, or replacing a `<textarea>` with `contenteditable`.

```css
textarea.compose {
    field-sizing: content;
    min-block-size: 3lh;
    max-block-size: 16lh;
    overflow-y: auto;
}
```

## Replaces

A common JavaScript loop:

```text
input event
 -> set height to auto/0
 -> read scrollHeight
 -> write height
```

The browser now owns intrinsic field sizing.

## Use it for

- chat/message composers
- comment boxes
- compact editable notes
- search/input controls that should shrink-wrap content

Always keep sensible `min-*` and `max-*` constraints. An indefinitely growing textarea is usually worse UX than a bounded textarea that becomes scrollable.

## Compatibility

MDN marks `field-sizing` as Baseline 2026, newly available across current browsers since June 2026. Firefox added it in Firefox 152, so it is newer than the Firefox 140 ESR engine used by Tor Browser 15.0.21.

Therefore:

```text
Firefox 152+/current browsers -> native autosize enhancement
Tor/Firefox 140 ESR           -> normal fixed-size textarea
```

The fallback remains a fully usable native form field.

## Sources

- MDN: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/field-sizing
- Firefox 152 release notes: https://developer.mozilla.org/en-US/docs/Mozilla/Firefox/Releases/152
- Low-level community signal: https://www.reddit.com/r/css/comments/1vz0mc4/
- Real product adoption discussion: https://github.com/thelounge/thelounge/issues/5105
