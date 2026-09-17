# Whole-Block Selection with `user-select: all`

**Role:** make a displayed credential/code block easy to select as one unit without clipboard JavaScript.

```html
<div class="recovery-phrase" tabindex="0">
  maple orbit velvet ...
</div>
```

```css
.recovery-phrase {
  user-select: all;
}
```

When selection starts inside the element, the browser expands selection to the whole element. This is useful for recovery phrases, IDs, commands and other short copyable blocks.

## Boundary

`user-select: all` is a **selection affordance**, not a Copy API. It does not write to the clipboard and should not be described as an automatic copy button.

If one-click clipboard writing is a hard requirement, that interaction is outside the PureDesign zero-client-JavaScript solution space. Keep the text visibly selectable and let the user use the browser/OS copy command instead.

Do not apply this to large prose regions where users may want partial selection.

## Accessibility

Do not make a non-interactive text block look like a button. If keyboard users benefit from focusing the block before selecting/copying, `tabindex="0"` can be used deliberately, but avoid adding unnecessary tab stops.

## Source

- https://developer.mozilla.org/en-US/docs/Web/CSS/user-select
