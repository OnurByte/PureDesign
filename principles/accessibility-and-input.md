# Accessibility and Input

Zero JavaScript does not automatically mean accessible.

## Rules

1. Preserve native semantics whenever possible.
2. Test keyboard interaction, not just mouse clicks.
3. Use `:focus-visible` for clear focus feedback.
4. Do not hide critical content behind hover-only behavior.
5. Treat touch, pointer and keyboard as distinct input paths.
6. Do not visually disable something without matching behavioral semantics.
7. Do not invent ARIA-heavy widgets when ordinary navigation/forms better match the task.
8. Native browser behavior still needs real UX testing with long content and assistive technology.

## Common examples

- `<details>` is preferable to a checkbox pretending to be a disclosure.
- `:user-invalid` often provides less hostile validation feedback than immediately styling every required field with `:invalid`.
- `<datalist>` is native but still has implementation/accessibility limitations; native does not mean universally suitable.
- `interestfor`/hint popovers are interesting because they move input-modality handling toward the browser, but they are not yet a conservative baseline.

## Principle

Prefer deleting custom interaction code by choosing a better semantic primitive, not by moving complexity into CSS selectors.
