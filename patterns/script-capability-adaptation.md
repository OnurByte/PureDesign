# Script-capability adaptation

## Goal

Embed PureDesign/no-JS components inside a larger application that may also contain optional script-only enhancements, without exposing dead controls when scripting is disabled.

## CSS capability gate

```css
.requires-script {
    display: none;
}

.no-script-note {
    display: block;
}

@media (scripting: enabled) {
    .requires-script {
        display: initial;
    }

    .no-script-note {
        display: none;
    }
}
```

## Rule

This is **not** permission to make PureDesign's core path depend on JS.

Use the media feature when a mixed host application has optional features that genuinely cannot operate without script, while the main task still has a native/server path.

Example:

```text
basic upload          -> native multipart form (always available)
optional drag/drop UI -> only exposed when its implementation exists
```

## Why not UA sniffing

The question is whether scripting is active, not whether the browser looks like Chrome/Firefox or whether a particular device is mobile.

## Read

- [`../primitives/scripting-media-feature.md`](../primitives/scripting-media-feature.md)
- [`../principles/progressive-enhancement.md`](../principles/progressive-enhancement.md)
