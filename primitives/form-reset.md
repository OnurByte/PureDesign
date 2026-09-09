# Native Form Reset

**Role:** reset a form to its initial control values without looping through fields in JavaScript.

```html
<form>
  ...
  <button type="reset">Reset form</button>
</form>
```

The browser restores form controls to their initial/default values.

## What this replaces

```text
querySelectorAll(inputs)
 -> read original/default values
 -> assign each value/check state
```

A low-visibility Reddit question asking how to loop through controls to restore defaults received the simpler answer: a real `type="reset"` button already does this.

## UX warning

Native does **not** mean recommended everywhere.

MDN specifically warns that reset buttons are often frustrating because users can accidentally erase substantial work. Do not add one to ordinary forms merely because the primitive exists.

Good candidates are narrow tools where “restore initial settings” is a clear, intentional action and the destructive effect is obvious.

## Boundary

Form-control reset -> browser.

Resetting durable saved application state -> server/application; a form reset does not undo a previously submitted change.

## Sources

- https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Structuring_content/HTML_forms
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input/reset
- Community example: https://www.reddit.com/r/webdev/comments/ysx03z/
