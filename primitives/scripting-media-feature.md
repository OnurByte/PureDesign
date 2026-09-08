# `@media (scripting: ...)`

**Role:** Stable capability-detection primitive.

The `scripting` media feature lets CSS detect whether scripting is active for the document without executing JavaScript.

```css
.js-only-affordance {
    display: none;
}

@media (scripting: enabled) {
    .js-only-affordance {
        display: initial;
    }
}

@media (scripting: none) {
    .no-js-help {
        display: block;
    }
}
```

Values:

- `none`
- `initial-only`
- `enabled`

## PureDesign use

A pure PureDesign surface should not require special fallback UI because core behavior already works without JS. This primitive becomes useful when PureDesign components are embedded inside a mixed application that also has optional script-enhanced features.

Use it to prevent a control whose only implementation is JavaScript from being presented when scripting is unavailable.

## Important limitation

Detection is based on browser settings. Some extensions block scripts in ways that may not be reflected perfectly by this media feature.

Do not use capability detection to weaken the baseline product contract.

## Compatibility

MDN marks the feature as widely available across browsers since December 2023, so it predates the Firefox 140 ESR baseline.

## Sources

- MDN: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/%40media/scripting
- CSS Baseline tooling example: https://github.com/eslint/css/blob/main/docs/rules/use-baseline.md
