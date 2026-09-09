# Server-Backed Image Coordinate Picker

Use [`<input type="image">`](../primitives/image-submit-coordinates.md) when clicking a known-size image should submit a point directly to the server, while preserving an equivalent non-pointing input path.

## Example

```html
<form action="/images/42/focus" method="post">
  <input type="hidden" name="image_version" value="8">

  <p id="point-help">
    Click the image to choose a focus point, or enter the coordinates below.
  </p>

  <div class="coordinate-canvas">
    <input
      type="image"
      name="point"
      src="/images/42/focus-source?v=8"
      alt="Choose a focus point on the image"
      width="640"
      height="360"
      aria-describedby="point-help">
  </div>

  <fieldset>
    <legend>Enter a point instead</legend>

    <label>
      X coordinate
      <input type="number" name="manual_x" min="0" max="639">
    </label>

    <label>
      Y coordinate
      <input type="number" name="manual_y" min="0" max="359">
    </label>

    <button type="submit" name="input_mode" value="manual">
      Set entered point
    </button>
  </fieldset>
</form>
```

```css
.coordinate-canvas {
  max-inline-size: 100%;
  overflow: auto;
}
```

The image itself keeps a known 640 × 360 CSS-pixel coordinate space. Smaller viewports scroll the containing region instead of silently rescaling the image and changing the server's coordinate interpretation.

## Server contract

When the image submitter was used, expect `point.x` and `point.y`. When the normal submit button was used, validate `manual_x` and `manual_y`.

The server must also verify that:

- the image/version still matches the coordinate space rendered to the user;
- coordinates are inside the expected range;
- the user may modify the referenced image;
- stale image revisions do not apply coordinates to a different geometry;
- `(0, 0)` is not blindly treated as proof of an intentional pointer selection when the submission path is ambiguous.

## When to use

Good bounded cases include:

- choosing an image focal point;
- selecting an approximate point on a fixed diagram;
- server-side color/pixel lookup demos;
- marking a point on a known-size map/image where an accessible alternative is provided.

## When not to use

Do not use this for a responsive image whose rendered dimensions vary while the server assumes intrinsic pixels.

Do not use it as the only interaction for a task that requires precise pointing: keyboard and assistive-technology users need the manual/structured path.

If the task is navigation among known regions rather than arbitrary coordinates, ordinary text links or a carefully designed client-side image map may be semantically better. Image maps themselves have responsiveness and accessibility tradeoffs; do not pick them merely because they are scriptless.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input/image
- https://developer.mozilla.org/en-US/docs/Web/HTML/How_to/Add_a_hit_map_on_top_of_an_image
