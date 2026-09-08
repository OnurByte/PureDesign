# `text-fit`

**Role:** emerging browser-native responsive text fitting without JavaScript text measurement loops.

It targets scripts that traditionally do:

```text
measure available box
 -> measure text
 -> binary-search font size
 -> react to resize
 -> set inline font size
```

The broader PureDesign rule is:

> Before measuring layout in JavaScript, check whether layout itself can own the problem.

## Status

Chrome 150-era feature; enhancement-only for conservative Firefox/Tor targets.

## Source

- https://developer.chrome.com/blog/new-in-chrome-150
