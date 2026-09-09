# Image Submit Coordinates (`<input type="image">`)

**Role:** let the browser submit the CSS-pixel coordinates where a graphical form submit control was activated, without a click handler.

```html
<form action="/image/focus" method="post">
  <input
    type="image"
    name="point"
    src="/images/photo.jpg"
    alt="Choose a focus point"
    width="640"
    height="360">
</form>
```

When the image is clicked, the browser submits two extra fields:

```text
point.x=<horizontal CSS-pixel coordinate>
point.y=<vertical CSS-pixel coordinate>
```

The origin is the top-left of the rendered image input.

## What this can replace

For a deliberately bounded server-backed coordinate action, this can replace:

```text
click listener
-> calculate offsetX / offsetY
-> create hidden fields
-> submit form
```

The browser already owns the submit action and coordinate serialization.

## Critical accessibility boundary

Do **not** make an exact coordinate task depend only on an image submit control.

Keyboard submission does not provide an equivalent pointing interaction; MDN documents `(0, 0)` as the default when submission occurs without a click. A server therefore cannot safely interpret every `(0, 0)` result as an intentional top-left pointer selection.

Provide an equivalent non-pointing path, such as:

- explicit X/Y number inputs;
- a semantic region `<select>` or radio group when exact pixels are unnecessary;
- another server-rendered form appropriate to the task.

Always provide meaningful `alt` text because the image is an interactive submit control.

## Geometry boundary

Submitted coordinates are relative to the **rendered** image control in CSS pixels, not automatically normalized percentages or intrinsic image pixels.

If CSS changes the rendered dimensions responsively, the server cannot infer that transformation from `point.x` / `point.y` alone.

Use this primitive only when the server can correctly interpret the rendered coordinate system, or collect enough explicit server-known geometry to perform the conversion. Do not silently combine a responsive `width: 100%` image with intrinsic-pixel server logic.

## Security

Coordinates are ordinary untrusted request values. Validate range and authorization server-side. Never let coordinate values bypass object ownership or image/version checks.

## Compatibility

`<input type="image">` is mature, widely supported HTML and may participate in core behavior on the conservative Firefox/Tor target when its accessibility and geometry constraints fit the product.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input/image
- https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Forms/Basic_native_form_controls
