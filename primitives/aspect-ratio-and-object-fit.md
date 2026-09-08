# `aspect-ratio` / `object-fit`

**Role:** let CSS size and crop media without JavaScript measurements.

```css
.preview {
  aspect-ratio: 16 / 9;
  overflow: hidden;
}

.preview > img,
.preview > video {
  inline-size: 100%;
  block-size: 100%;
  object-fit: cover;
}
```

`aspect-ratio` gives the layout engine a preferred width/height relationship. `object-fit` controls how replaced content such as images/video is fit inside that box.

## Replaces

- resize listeners that recompute media box height;
- image-load handlers whose only job is maintaining a ratio;
- canvas-like cropping logic for ordinary cover/contain presentation.

When intrinsic media dimensions are known, also include HTML `width`/`height` attributes to reserve space before the resource loads.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/aspect-ratio
- https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/object-fit
