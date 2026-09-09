# Native Lazy Loading — Important No-JS Caveat

HTML exposes native deferred-loading hints such as:

```html
<img src="/img/preview.jpg" loading="lazy" alt="Preview">
<iframe src="/embed" loading="lazy" title="Embed"></iframe>
<video src="/media/demo.webm" controls loading="lazy"></video>
<audio src="/media/demo.ogg" controls loading="lazy"></audio>
```

Chrome 148 expanded native lazy loading to `<video>` and `<audio>`. These hints can replace `IntersectionObserver`-based lazy loaders in ordinary scripting-enabled pages.

## Critical PureDesign rule

**Do not count `loading="lazy"` as a network-saving feature when the product contract is JavaScript disabled.**

MDN documents that native lazy loading is only deferred when JavaScript is enabled. This is an anti-tracking measure: otherwise a server could infer approximate scroll position from the timing of lazy resource requests even when scripting is disabled.

Therefore:

```text
loading=lazy present
        ≠
request definitely deferred in a no-JS browser
```

You may still include the attribute as progressive performance metadata, but capacity/bandwidth planning for a strict no-JS page must assume that this optimization can disappear.

## Media caveat

A lazy-loaded audio element must have visible geometry for viewport proximity to make sense; native `controls` provide that in the ordinary no-custom-player case.

Do not hide a media element and expect `loading="lazy"` to become a reliable no-JS preloading scheduler.

## Related

For large server-rendered documents, [content-visibility](content-visibility.md) can reduce rendering work but likewise does not remove the resource/DOM payload.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/Performance/Guides/Lazy_loading
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/img
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/iframe
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/video
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/audio
- https://developer.chrome.com/release-notes/148
