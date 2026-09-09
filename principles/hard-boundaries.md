# Hard Boundaries of Zero-Client-JavaScript UI

PureDesign is intentionally not a challenge to encode an application runtime in CSS.

Some browser tasks do not currently have a semantic HTML/CSS/form/URL/server-rendered path with equivalent behavior. When one of these boundaries applies, change the interaction model or document the limitation instead of inventing a fake CSS state machine.

## Client-only file inspection before upload

A native file input can select files, but CSS/HTML cannot read the selected file bytes, create an object URL, inspect EXIF metadata, hash the file, or render a local preview before a request.

```text
possible:   select file -> submit multipart -> server returns preview
not native: select file -> inspect/render local bytes before submission
```

See [`primitives/native-file-upload.md`](../primitives/native-file-upload.md).

## Custom drag-and-drop reordering with durable order

CSS can visually reorder layout, but it does not turn arbitrary pointer dragging into a persisted application ordering operation.

Prefer explicit server actions such as Move up / Move down, position selects, or another form workflow when ordering must remain zero-JS.

Do not use visual `order`/grid placement to pretend durable data order changed.

## Fetch-on-input / remote autocomplete without navigation

A static [`<datalist>`](../primitives/datalist.md) can provide document-supplied suggestions. HTML does not automatically perform arbitrary remote requests on every keystroke and merge the result into a custom combobox.

For remote search/filter suggestions, use a submitted GET form and server-rendered response. If a bounded inline response is appropriate, [`patterns/server-backed-inline-result-panel.md`](../patterns/server-backed-inline-result-panel.md) can target a child browsing context after explicit submission.

## Arbitrary client computation from form fields

CSS may derive presentation from browser state, attributes, selectors and newer value functions. It is not an application calculator.

Business totals, permissions, pricing, cryptographic work, dependent data lookups and authoritative validation belong to the server unless a native form control already owns the exact behavior.

A server roundtrip is a valid PureDesign solution.

## Script-produced capability results

Emerging permission controls can move geolocation/camera/microphone permission UI into HTML, but returned position or `MediaStream` objects still require DOM API/event consumption for most application workflows.

See [`primitives/capability-elements-watchlist.md`](../primitives/capability-elements-watchlist.md).

Do not claim a complete no-JS location/camera workflow merely because the permission button is declarative.

## Rich custom widgets with required keyboard state machines

ARIA does not implement interaction behavior.

A custom combobox, editable grid, application-style tree, roving-focus toolbar or similar APG widget may require keyboard/focus state that ordinary HTML does not provide for that custom semantic model.

Prefer a native control, disclosure, links/forms, or simpler document structure. If the expected widget behavior cannot be provided without event handling, the custom widget is outside PureDesign.

See [`principles/accessibility-and-input.md`](accessibility-and-input.md).

## Scroll-triggered data fetching / infinite scroll

CSS can observe or style scroll state and can drive decorative animation, but conservative browsers do not natively fetch arbitrary next-page application data because the user crossed a scroll threshold.

Use ordinary pagination, a Load more link/form, or server-rendered navigation. Declarative partial-update mechanisms remain future research; see [`primitives/declarative-partial-updates.md`](../primitives/declarative-partial-updates.md).

## In-page upload/request progress controlled by application bytes

`<progress>` can represent a value that the document already knows, but HTML/CSS cannot continuously mutate its value from XMLHttpRequest/fetch upload events because those are scripting APIs.

Do not show a fake CSS timer as upload progress. Use normal browser navigation/network affordances, a server response after completion, or another non-browser client for resumable/chunked transfers.

## Client-only durable storage

CSS/browser ephemeral interaction state is not a durable application database.

PureDesign durable state belongs to URLs/server data. Browser preferences such as color scheme can be observed, but arbitrary application state cannot be written to `localStorage`/IndexedDB without script.

For user-selected durable settings, submit a form and persist them server-side or encode safe shareable state in a URL where appropriate.

## Automatic submission on arbitrary field change

A normal form submits from an explicit submit action (or browser-defined form behavior). CSS cannot turn every arbitrary `change`/`input` event into a network request.

If changing one field must update dependent choices, add an explicit Update/Continue submitter and let the server render the next state.

Do not hide a submit button and imply the page has live dependency updates when it does not.

## Arbitrary parent-document DOM patching

A targeted iframe can navigate its own browsing context, but it does not replace arbitrary nodes in the parent document. CSS likewise cannot parse a server response and patch the parent DOM.

Use a normal server-rendered navigation, a clearly bounded named-frame result panel, or wait for a genuinely declarative platform primitive whose compatibility matches the target.

## Decision rule

When a requested interaction reaches one of these boundaries:

```text
1. look for a real native semantic equivalent
2. change the interaction to URL/form/server navigation if possible
3. keep experimental browser features enhancement-only
4. if equivalent behavior still requires client event/data code: mark unsupported
```

The goal is a smaller, more truthful architecture — not CSS that secretly behaves like a worse JavaScript runtime.
