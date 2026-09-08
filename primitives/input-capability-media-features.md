# Input-capability media features

**Role:** Stable adaptive-input primitive.

CSS can query what kind of pointing/hover interaction the user's input devices support, avoiding JavaScript device heuristics such as user-agent sniffing or `ontouchstart` checks.

Relevant media features:

- `hover`
- `any-hover`
- `pointer`
- `any-pointer`

```css
/* Baseline works for touch/keyboard. */
.action-description {
    display: block;
}

/* Add hover-only polish only when convenient hover exists. */
@media (hover: hover) and (pointer: fine) {
    .card:hover {
        transform: translateY(-1px);
    }
}
```

## Use it for

- avoiding hover-dependent affordances on touch-first devices
- increasing target/padding for coarse pointers
- enabling hover-only decoration without making hover mandatory
- choosing interaction density based on input capability rather than screen width

## Rule

Never infer accessibility needs or device identity from these queries. A large screen can have touch input; a small device can have a mouse; users can have multiple input mechanisms.

Keyboard interaction must remain independently correct.

## Sources

- MDN `hover`: https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/%40media/hover
- MDN media feature index (`pointer`, `any-pointer`, `any-hover`): https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/%40media
