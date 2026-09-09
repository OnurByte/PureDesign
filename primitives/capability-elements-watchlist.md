# Capability Elements — Watchlist

Emerging HTML Capability Elements move permission prompts and user intent toward browser-owned controls.

Examples include:

- `<geolocation>` for location access;
- `<usermedia>` for camera/microphone stream access;
- newer specialized camera/microphone controls as the proposal family evolves.

These are interesting for PureDesign, but **they are not currently a complete zero-client-JavaScript application primitive**.

## Why not yet?

`<geolocation>` can render a browser-defined control and perform the permission/data-retrieval flow. The resulting position is exposed through the `HTMLGeolocationElement.position` DOM property and a `location` event.

`<usermedia>` similarly mediates permission and provides a `MediaStream` object to the application.

That means the browser can own substantially more of the permission UX, but an application still needs client code to consume the returned object for tasks such as:

- submitting latitude/longitude in a form;
- drawing a local map from the returned coordinates;
- attaching a returned media stream to an application workflow;
- recording/processing that stream.

Under PureDesign's contract:

```text
declarative permission control
        !=
serializable no-JS form result
```

Do not claim that a location picker, camera capture flow or microphone recorder has become PureDesign-compatible merely because the permission button itself is declarative.

## Fallback content is not data plumbing

Capability elements may contain fallback content for unsupported browsers. That helps communicate or provide an alternate route, but it does not make the returned capability data available to a normal HTML form.

A server-backed alternative may still exist for a specific product—for example asking the user to type an address or upload an already-captured file—but that is a different interaction.

## Compatibility

This family is experimental and Chromium-led in the 2026-09 snapshot. It is not core for Firefox 140 ESR / Tor Browser.

Revisit this watchlist if the platform gains declarative form participation or another scriptless way to serialize capability results.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/geolocation
- https://developer.mozilla.org/en-US/docs/Web/API/HTMLGeolocationElement/position
- https://developer.chrome.com/blog/usermedia-html-element
