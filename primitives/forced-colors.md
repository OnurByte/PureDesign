# `forced-colors`

**Role:** adapt small UI details when the browser enforces a user-chosen limited/high-contrast palette.

```css
.button {
  box-shadow: 0 0 0 1px rgb(0 0 0 / .2);
}

@media (forced-colors: active) {
  .button {
    border: 2px solid ButtonBorder;
  }
}
```

In forced-colors mode, browsers replace many author colors at paint time and remove effects such as `box-shadow`/`text-shadow`. CSS system-color keywords such as `CanvasText`, `ButtonText`, and `ButtonBorder` integrate with the user palette.

## Rule

Do not fight forced-colors mode or broadly set `forced-color-adjust: none`. The user's palette may be essential for readability. Use the media query only for targeted fixes where browser forcing otherwise removes an important boundary/state cue.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/At-rules/%40media/forced-colors
- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/forced-color-adjust
- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/system-color
