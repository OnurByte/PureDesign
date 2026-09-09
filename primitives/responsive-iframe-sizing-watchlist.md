# Responsive `<iframe>` Content Sizing — Watchlist

**Role:** future/progressive browser-owned sizing of an `<iframe>` from the embedded document's intrinsic layout size, without parent-side measurement scripts.

The emerging composition is double opt-in.

Embedding document:

```css
.result-frame {
  frame-sizing: content-block-size;
}
```

Embedded document:

```html
<meta name="responsive-embedded-sizing">
```

The embedded document opts in to sharing its layout size and the parent asks the frame to size from that content.

## Why this matters

Today a common iframe integration does this in JavaScript:

```text
measure child document
-> postMessage / same-origin read
-> set iframe height
-> repeat when content changes
```

`frame-sizing` is intended to move the initial sizing handshake into the platform while preserving a privacy/security opt-in boundary.

## PureDesign boundary

This feature is **not currently shippable as a conservative PureDesign dependency**.

Current implementations are experimental / behind flags and there is no stable interoperable baseline. Use a conventional explicit/minimum iframe size with internal scrolling today.

The platform also exposes `Window.requestResize()` for later dynamic size changes, but calling that method is JavaScript and therefore is not part of a PureDesign implementation. The useful PureDesign subset is browser-reported initial/load sizing when and where that behavior ships declaratively.

## Privacy model

An iframe does not normally reveal its content dimensions to the embedding page. Responsive embedded sizing therefore requires the child document to opt in with the meta element.

Do not treat cross-origin content sizing as free ambient information.

## Fallback

```css
.result-frame {
  inline-size: 100%;
  block-size: 28rem;
}

@supports (frame-sizing: content-block-size) {
  .result-frame {
    frame-sizing: content-block-size;
  }
}
```

Even this support query should be treated as future-facing until stable browser support exists.

## Compatibility

As of 2026-09, current stable Firefox, Safari and Chromium do not provide an interoperable enabled-by-default baseline. Chromium builds expose the feature behind flags in newer versions.

Never make content access depend on automatic frame sizing.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/frame-sizing
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/meta/name/responsive-embedded-sizing
- https://github.com/w3c/csswg-drafts/blob/main/css-sizing-4/responsive-iframes-explainer.md
