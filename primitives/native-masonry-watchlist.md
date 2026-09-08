# Native CSS Masonry / Grid Lanes — Watchlist

**Status:** not a conservative production primitive as of the 2026-09 research snapshot.

Browser vendors are actively developing native masonry/grid-lanes layout, but syntax/spec direction has changed during development.

Chrome/Edge exposed early developer testing from Chromium 140, and Chrome's own documentation warns that older examples use outdated syntax compared with the newer Grid Lanes direction.

## PureDesign rule

Do not copy experimental masonry syntax into core styles just because a browser flag/demo supports it.

Use a stable fallback whose semantic reading order is acceptable, then progressively replace it when native masonry becomes interoperable.

Potential fallbacks:

- ordinary CSS Grid for card layouts;
- multi-column layout for content where down-column reading order is correct;
- server-computed layout only when exact placement is genuinely required.

## Sources

- https://developer.chrome.com/blog/masonry-update
- https://drafts.csswg.org/css-grid-3/
